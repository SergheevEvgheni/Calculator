<template>
  <div class="row">
    <div class="col-8 offset-2 my-5 card">
      <div class="card-body">
        <h1 class="card-title col-12 text-center mb-4">Numpad Control Panel</h1>
        <div class="row">
          <div class="col-4">
            <div class="row">
              <NumpadCheckbox
                :checked="isNumpadLeftHanded"
                label="Left Handed Mode"
                @update:checked="isNumpadLeftHanded = $event"
              />
            </div>
            <div class="row">
              <NumpadCheckbox
                :checked="isNumpadDisabled"
                label="Disable Numpad"
                @update:checked="isNumpadDisabled = $event"
              />
            </div>
          </div>
          <div class="col-4">
            <NumpadSelect
              :value="layout"
              :layout-types="layoutTypes"
              @update:value="layout = $event"
            />
          </div>
          <div class="col-4"></div>
        </div>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col-12">
      <Numpad
        :is-numpad-left-handed="isNumpadLeftHanded"
        :layout="layout"
        :layout-types="layoutTypes"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, provide } from 'vue'
import Numpad from '@/components/Numpad.vue'
import NumpadCheckbox from '@/components/interface/NumpadCheckbox.vue'
import NumpadSelect from '@/components/interface/NumpadSelect.vue'

export default defineComponent({
  name: 'NumpadWrapper',
  components: {
    Numpad,
    NumpadCheckbox,
    NumpadSelect
  },
  setup () {
    const layoutTypes = {
      default: 'Default',
      numberOnly: 'Numbers only',
      numbersRemove: 'Numbers + Remove',
      currencyChanger: 'Currency Changer'
    }

    const isNumpadLeftHanded = ref(false)
    const isNumpadDisabled = ref(false)
    const layout = ref(layoutTypes.default)

    provide('isNumpadDisabled', isNumpadDisabled)

    return {
      isNumpadLeftHanded,
      isNumpadDisabled,
      layoutTypes,
      layout
    }
  }
})
</script>

<style scoped lang="scss">

</style>
