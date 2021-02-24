<template>
  <button
    type="button"
    class="btn"
    :class="`btn--${buttonType}`"
    @click="$emit('btnClick', value)"
  >
    <slot>{{ value }}</slot>
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NumpadButton',
  props: {
    buttonType: {
      type: String,
      required: true
    },
    value: {
      type: String,
      required: false
    }
  },
  emits: ['btnClick']
})
</script>

<style scoped lang="scss">
.btn {
  box-sizing: border-box;
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
