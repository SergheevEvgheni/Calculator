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
        :are-screen-and-operators-visible="areScreenAndOperatorsVisible"
        :is-remove-button-visible="isRemoveButtonVisible"
        :is-currency-changer-visible="isCurrencyChangerVisible"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, provide, computed } from 'vue'
import Numpad from '@/components/Numpad.vue'
import NumpadCheckbox from '@/components/interface/NumpadCheckbox.vue'
import NumpadSelect from '@/components/interface/NumpadSelect.vue'
import { LayoutTypes } from '@/enums'

export default defineComponent({
  name: 'NumpadWrapper',
  components: {
    Numpad,
    NumpadCheckbox,
    NumpadSelect
  },
  setup () {
    const isNumpadLeftHanded = ref(false)
    const isNumpadDisabled = ref(false)
    const layout = ref(LayoutTypes.default)

    provide('isNumpadDisabled', isNumpadDisabled)

    const areScreenAndOperatorsVisible = computed(() => {
      return layout.value === LayoutTypes.default || layout.value === LayoutTypes.currencyChanger
    })
    const isRemoveButtonVisible = computed(() => {
      return layout.value === LayoutTypes.numbersRemove
    })
    const isCurrencyChangerVisible = computed(() => {
      return layout.value === LayoutTypes.currencyChanger
    })

    return {
      isNumpadLeftHanded,
      isNumpadDisabled,
      layout,
      areScreenAndOperatorsVisible,
      isRemoveButtonVisible,
      isCurrencyChangerVisible
    }
  }
})
</script>
