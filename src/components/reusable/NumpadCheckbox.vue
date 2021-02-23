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
    checked: Boolean,
    label: String
  }
})
</script>
