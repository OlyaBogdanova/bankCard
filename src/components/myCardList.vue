<template lang="">
  <div class="card-list">
    <div class="card-item" :class="{ '-active': isCardFlipped }">
      <myCardItemFront />
      <myCardItemSide />
    </div>
  </div>
</template>
<script>
import { inject, computed, provide } from 'vue'
import myCardItemFront from './myCardItemFront.vue'
import myCardItemSide from './myCardItemSide.vue'

export default {
  components: { myCardItemFront, myCardItemSide },

  setup() {
    const isCardFlipped = inject('isCardFlipped')
    const currentCardBackground = computed(() => {
      return Math.floor(Math.random() * 25 + 1)
    })
    provide('currentCardBackground', currentCardBackground)
    return { isCardFlipped }
  }
}
</script>
<style lang=""></style>
