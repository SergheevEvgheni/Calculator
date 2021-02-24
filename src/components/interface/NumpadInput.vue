<template>
  <div class="input-group my-3">
    <span
      class="input-group-text"
      id="basic-addon1"
    >
      {{ label }}
    </span>
    <input
      :value="value"
      type="text"
      class="form-control"
      aria-label="Username"
      @change="$emit('update:value', $event.target.value)"
    >
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NumpadInput',
  props: {
    value: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    }
  },
  emits: ['update:value']
})
</script>
