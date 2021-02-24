<template>
  <select
    :value="value"
    class="form-select mt-2"
    aria-label="Default"
    @change="$emit('update:value', $event.target.value)"
  >
    <option
      v-for="type in LayoutTypes"
      :key="type"
      :value="type"
    >
      {{ type }}
    </option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { LayoutTypes } from '@/enums'

export default defineComponent({
  name: 'NumpadSelect',
  props: {
    value: {
      type: String,
      required: true
    }
  },
  setup () {
    return {
      LayoutTypes
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
