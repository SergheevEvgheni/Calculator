<template>
  <select
    :value="view"
    class="form-select"
    aria-label="Default"
    @change="$emit('update:view', $event.target.value)"
  >
    <option>Default</option>
    <option>Numbers only</option>
    <option>Numbers + Remove</option>
    <option>Currency Changer</option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NumpadSelect',
  props: {
    view: String
  }
})
</script>

<style scoped lang="scss">

</style>
