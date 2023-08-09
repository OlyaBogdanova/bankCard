<template lang="">
  <div class="card-list">
    <div class="card-item" :class="{ '-active': isCardFlipped }">
      <myCardItemFront />
      <myCardItemSide />
    </div>
  </div>
</template>
<script>
import { ref, provide, inject } from 'vue'
import myCardItemFront from './myCardItemFront.vue'
import myCardItemSide from './myCardItemSide.vue'

export default {
  components: { myCardItemFront, myCardItemSide },

  setup() {
    const isCardFlipped = inject('isCardFlipped')
    return { isCardFlipped }
  }
}
</script>
<style lang=""></style>
