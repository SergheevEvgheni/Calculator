<template>
  <div class="form-check form-switch">
    <input
      :checked="checked"
      :id="label"
      class="form-check-input"
      type="checkbox"
      @change="$emit('update:checked', !checked)"
    >
    <label
      class="form-check-label"
      :for="label"
    >
      {{ label }}
    </label>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NumpadCheckbox',
  props: {
    checked: {
      type: Boolean,
      required: true
    },
    label: {
      type: String,
      required: true
    }
  },
  emits: ['update:checked']
})
</script>

<style lang="scss" scoped>
  .form-switch {
    font-size: 1.4rem;
  }
</style>
