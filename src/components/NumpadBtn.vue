<template>
  <button
    type="button"
    class="btn"
    :class="`btn--${btnStyle}`"
  >
    <slot />
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NumpadBtn',
  props: {
    btnStyle: String
  },
  setup (props) {
    console.log(props)
  }
})
</script>

<style scoped lang="scss">

  .btn {
    &--number {
      background-color: #424242;
      color: #fff;
      &:hover {
        color: #fff;
      }
    }
    &--operator {
      background-color: #fff;
      color: #424242;
      border: 2px solid #424242;
    }
    &--check {
      flex: 1;
      background-color: #93D300;
      color: #fff;
      border: none;
      &:hover {
        color: #fff;
      }
    }
  }
</style>
