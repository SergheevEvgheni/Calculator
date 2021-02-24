<template>
  <div class="input-group mb-3 mt-2">
    <span
      class="input-group-text"
      id="basic-addon1"
    >
      {{ label }}
    </span>
    <input
      :value="value"
      type="number"
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
      type: Number,
      required: true
    },
    label: {
      type: String,
      required: true
    }
  }
})
</script>

<style scoped lang="scss">

</style>
