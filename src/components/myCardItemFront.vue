<template>
  <div class="card-item__side -front">
    <div
      class="card-item__focus"
      :class="{ '-active': focusElementStyle }"
      :style="focusElementStyle"
      ref="focusElement"
    ></div>
    <div class="card-item__cover">
      <img
        :src="
          'https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/' +
          currentCardBackground +
          '.jpeg'
        "
        class="card-item__bg"
      />
    </div>

    <div class="card-item__wrapper">
      <div class="card-item__top">
        <img
          src="https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/chip.png"
          class="card-item__chip"
        />
        <div class="card-item__type">
          <transition name="slide-fade-up">
            <img
              :src="
                'https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/' +
                getCardType +
                '.png'
              "
              v-if="getCardType"
              :key="getCardType"
              alt=""
              class="card-item__typeImg"
            />
          </transition>
        </div>
      </div>
      <label for="cardNumber" class="card-item__number" >
        <template v-if="getCardType === 'amex'">
          <span v-for="(n, index) in amexCardMask" :key="index">
            <transition name="slide-fade-up">
              <div
                class="card-item__numberItem"
                v-if="$index > 4 && index < 14 && cardNumber.length > index && n.trim() !== ''"
              >
                *
              </div>
              <div
                class="card-item__numberItem"
                :class="{ '-active': n.trim() === '' }"
                :key="index"
                v-else-if="cardNumber.length > index"
              >
                {{ cardNumber[index] }}
              </div>
              <div
                class="card-item__numberItem"
                :class="{ '-active': n.trim() === '' }"
                v-else
                :key="index + 1"
              >
                {{ n }}
              </div>
            </transition>
          </span>
        </template>

        <div v-else>
          <span v-for="(n, index) in otherCardMask" :key="index">
            <transition name="slide-fade-up">
              <div
                class="card-item__numberItem"
                v-if="$index > 4 && $index < 15 && cardNumber.length > $index && n.trim() !== ''"
              >
                *
              </div>
              <div
                class="card-item__numberItem"
                :class="{ '-active': n.trim() === '' }"
                :key="$index"
                v-else-if="cardNumber.length > $index"
              >
                {{ cardNumber[$index] }}
              </div>
              <div
                class="card-item__numberItem"
                :class="{ '-active': n.trim() === '' }"
                v-else
                :key="$index + 1"
              >
                {{ n }}
              </div>
            </transition>
          </span>
        </div>
      </label>
      <div class="card-item__content">
        <label for="cardName" class="card-item__info" id="cardName">
          <div class="card-item__holder">Card Holder</div>
          <transition name="slide-fade-up">
            <div class="card-item__name" v-if="cardName.length" key="1">
              <transition-group name="slide-fade-right">
               <div    v-if="$index === $index">
                <span
                  class="card-item__nameItem"
                  v-for="(n, $index) in cardName.replace(/\s\s+/g, ' ')"
                  :key="$index + 1"
                  >{{ n }}</span
                >
               </div>
              </transition-group>
            </div>
            <div class="card-item__name" v-else key="2">Full Name</div>
          </transition>
        </label>
        <div class="card-item__date" ref="cardDate" id="cardDate">
          <label for="cardMonth" class="card-item__dateTitle">Expires</label>
          <label for="cardMonth" class="card-item__dateItem">
            <transition name="slide-fade-up">
              <span v-if="cardMonth" v-bind:key="cardMonth">{{ cardMonth }}</span>
              <span v-else key="2">MM</span>
            </transition>
          </label>

          <label for="cardYear" class="card-item__dateItem">
            <transition name="slide-fade-up">
              <span v-if="cardYear" :key="cardYear">{{ String(cardYear).slice(2, 4) }}</span>
              <span v-else key="2">YY</span>
            </transition>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, inject } from 'vue'
export default {
  setup() {
    const focusElementStyle = inject('focusElementStyle')
    const getCardType = inject('getCardType')
    const cardNumber = inject('cardNumber')
    const cardName = inject('cardName')
    const cardMonth = inject('cardMonth')
    const cardYear = inject('cardYear')
    const cardCvv = inject('cardCvv')
    const otherCardMask = '#### #### #### ####'

    const currentCardBackground = computed(() => {
      return Math.floor(Math.random() * 25 + 1)
    })

    return {
        currentCardBackground, focusElementStyle, getCardType, cardNumber, cardName, cardMonth, cardYear, cardCvv,  otherCardMask 
    }
  }
}
</script>
<style lang=""></style>
