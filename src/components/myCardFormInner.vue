<template>
  <div class="card-form__inner">
    <div class="card-input">
      <label for="cardNumber" class="card-input__label">Card Number</label>
      <input
        type="text"
        id="cardNumber"
        @input="formatCreditCardNumber"
        @keydown="handleKeyDown"
        maxlength="19"
        class="card-input__input"
        v-model="cardNumber"
        @focus="focusInput"
        @blur="blurInput"
        data-ref="cardNumber"
        autocomplete="off"
      />
    </div>
    <div class="card-input">
      <label for="cardName" class="card-input__label">Card Holders</label>
      <input
        type="text"
        id="cardName"
        class="card-input__input"
        v-model="cardName"
        @focus="focusInput"
        @blur="blurInput"
        data-ref="cardName"
        autocomplete="off"
      />
    </div>
    <div class="card-form__row">
      <div class="card-form__col">
        <div class="card-form__group">
          <label for="cardMonth" class="card-input__label">Expiration Date</label>
          <select
            class="card-input__input -select"
            id="cardMonth"
            v-model="cardMonth"
            @focus="focusInput"
            @blur="blurInput"
            data-ref="cardDate"
          >
            <option value="" disabled selected>Month</option>
            <option
              :value="n < 10 ? '0' + n : n"
              v-for="n in 12"
              :disabled="n < minCardMonth"
              :key="n"
            >
              {{ n < 10 ? '0' + n : n }}
            </option>
          </select>
          <select
            class="card-input__input -select"
            id="cardYear"
            v-model="cardYear"
            @focus="focusInput"
            @blur="blurInput"
            data-ref="cardDate"
          >
            <option value="" disabled selected>Year</option>
            <option :value="$index + minCardYear" v-for="(n, $index) in 12" :key="n">
              {{ $index + minCardYear }}
            </option>
          </select>
        </div>
      </div>
      <div class="card-form__col -cvv">
        <div class="card-input">
          <label for="cardCvv" class="card-input__label">CVV</label>
          <input
            type="text"
            class="card-input__input"
            id="cardCvv"
            data-maska="'####'"
            maxlength="3"
            v-model="cardCvv"
            @focus="flipCard(true)"
            @blur="flipCard(false)"
            autocomplete="off"
          />
        </div>
      </div>
    </div>

    <button class="card-form__button">Submit</button>
  </div>
</template>
<script>
import { inject, onMounted, ref, computed, watch, reactive } from 'vue'
export default {
  setup() {
    const focusElementStyle = inject('focusElementStyle')
    const getCardType = inject('getCardType')
    const cardNumber = inject('cardNumber')
    const cardName = inject('cardName')
    const cardMonth = inject('cardMonth')
    const cardYear = inject('cardYear')
    const cardCvv = inject('cardCvv')
    const isCardFlipped = inject('isCardFlipped')
    const minCardYear = new Date().getFullYear()
    const otherCardMask = '#### #### #### ####'
    const cardNumberTemp = ref('')
    const isInputFocused = ref(false)

    onMounted(() => {
      cardNumberTemp.value = otherCardMask
    })

    const generateCardNumberMask = computed(() => {
      return otherCardMask
    })

    const minCardMonth = computed(() => {
      if (cardYear.value === minCardYear) return new Date().getMonth() + 1
      return 1
    })

    function flipCard(status) {
      console.log(isCardFlipped)
      isCardFlipped.value = status
    }

    function focusInput(e) {
      isInputFocused.value = true
      let targetRef = e.target.dataset.ref
      let target = document.getElementById(targetRef)
      focusElementStyle.value = {
        width: `${target.offsetWidth}px`,
        height: `${target.offsetHeight}px`,
        transform: `translateX(${target.offsetLeft}px) translateY(${target.offsetTop}px)`
      }
    }
    function formatCreditCardNumber() {
      cardNumber.value = cardNumber.value
        .replace(/\D/g, '')
        .replace(/(.{4})/g, '$1 ')
        .trim()
    }
    function handleKeyDown(event) {
      if (!/^\d$|^Backspace$|^Delete$/.test(event.key)) {
        event.preventDefault()
      }
    }
    function blurInput() {
      setTimeout(() => {
        if (!isInputFocused.value) {
          focusElementStyle.value = null
        }
      }, 300)
      isInputFocused.value = false
    }

    watch(cardYear, () => {
      if (cardMonth.value < minCardMonth.value) {
        cardMonth.value = ''
      }
    })

    return {
      focusElementStyle,
      getCardType,
      cardCvv,
      cardMonth,
      cardName,
      cardNumber,
      cardYear,
      isCardFlipped,
      flipCard,
      minCardMonth,
      minCardYear,
      blurInput,
      focusInput,
      generateCardNumberMask,
      formatCreditCardNumber,
      handleKeyDown
    }
  }
}
</script>

<style lang="css"></style>
