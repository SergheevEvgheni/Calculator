<template>
  <select
    :value="value"
    class="form-select mt-2"
    aria-label="Default"
    @change="$emit('update:value', $event.target.value)"
  >
    <option
      v-for="type in layoutTypes"
      :key="type"
      :value="type"
    >
      {{ type }}
    </option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NumpadSelect',
  props: {
    value: {
      type: String,
      required: true
    },
    layoutTypes: {
      type: Object,
      required: true
    }
  }
})
</script>

<style scoped lang="scss">
  .form-select {
    text-align: center;
    font-size: 1.4rem;
  }
</style>
