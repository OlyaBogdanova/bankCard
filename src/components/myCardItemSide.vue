<template lang="">
  <div class="card-item__side -back">
    <div class="card-item__cover">
      <img
        v-bind:src="
          'https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/' +
          currentCardBackground +
          '.jpeg'
        "
        class="card-item__bg"
      />
    </div>
    <div class="card-item__band"></div>
    <div class="card-item__cvv">
      <div class="card-item__cvvTitle">CVV</div>
      <div class="card-item__cvvBand">
        <span v-for="(n, $index) in cardCvv" :key="$index"> * </span>
      </div>
      <div class="card-item__type">
        <img
          v-bind:src="
            'https://raw.githubusercontent.com/muhammederdem/credit-card-form/master/src/assets/images/' +
            getCardType +
            '.png'
          "
          v-if="getCardType"
          class="card-item__typeImg"
        />
      </div>
    </div>
  </div>
</template>
<script>
import { inject } from 'vue'
export default {
  setup() {
    const cardCvv = inject('cardCvv')
    const getCardType = inject('getCardType')
    const isCardFlipped = inject('isCardFlipped')
    const currentCardBackground=inject('currentCardBackground')
    return {
      cardCvv,
      getCardType,
      isCardFlipped,
      currentCardBackground
    }
  }
}
</script>
<style lang=""></style>
