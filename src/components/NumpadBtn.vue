<template>
  <button
    type="button"
    class="btn"
    :class="`btn--${btnStyle}`"
    @click="$emit('btnClick', value)"
  >
    <slot>{{ value }}</slot>
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NumpadBtn',
  props: {
    btnStyle: String,
    value: String
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
