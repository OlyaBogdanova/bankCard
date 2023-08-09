<script setup>
import myCardList from './components/myCardList.vue'
import MyCardFormInner from './components/myCardFormInner.vue'
import { ref, computed, provide } from 'vue'

const focusElementStyle = ref(null)
const cardNumber = ref('')
const cardName = ref('')
const cardMonth = ref('')
const cardYear = ref('')
const cardCvv = ref('')
const isCardFlipped = ref(false)

const getCardType = computed(() => {
  let number = cardNumber.value
  let re = new RegExp('^4')
  if (number.match(re) != null) {
    return 'visa'
  }

  re = new RegExp('^(34|37)')
  if (number.match(re) != null) {
    return 'amex'
  }

  re = new RegExp('^5[1-5]')
  if (number.match(re) != null) {
    return 'mastercard'
  }

  re = new RegExp('^6011')
  if (number.match(re) != null) {
    return 'discover'
  }

  re = new RegExp('^9792')
  if (number.match(re) != null) {
    return 'troy'
  }

  return 'visa' // default type
})

provide('focusElementStyle', focusElementStyle)
provide('getCardType', getCardType)
provide('cardNumber', cardNumber)
provide('cardName', cardName)
provide('cardMonth', cardMonth)
provide('cardYear', cardYear)
provide('cardCvv', cardCvv)
provide('isCardFlipped', isCardFlipped)
</script>

<template>
  <div><myCardList /><MyCardFormInner /></div>
</template>

<style></style>
