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
          <div class="col-4 mt-2">
            <NumpadSelect
              :value="layout"
              @update:value="layout = $event"
            />
          </div>
          <div class="col-4">
            <div class="row mt-2">
              <div class="col-6">
                <NumpadInput
                  :value="minimumValue"
                  label="Min Value"
                  @update:value="minimumValue = $event"
                />
              </div>
             <div class="col-6">
               <NumpadInput
                 :value="maximumValue"
                 label="Max Value"
                 @update:value="maximumValue = $event"
               />
             </div>
            </div>
          </div>
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
        :minimum-value="minimumValue"
        :maximum-value="maximumValue"
        :formatter="formatter"
        @confirm="onNumpadConfirm"
        @currency-change="onCurrencyChange"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, provide, computed } from 'vue'
import Numpad from '@/components/Numpad.vue'
import NumpadCheckbox from '@/components/interface/NumpadCheckbox.vue'
import NumpadSelect from '@/components/interface/NumpadSelect.vue'
import NumpadInput from '@/components/interface/NumpadInput.vue'
import { LayoutTypes } from '@/enums'

export default defineComponent({
  name: 'NumpadControl',
  components: {
    Numpad,
    NumpadCheckbox,
    NumpadSelect,
    NumpadInput
  },
  setup () {
    const isNumpadLeftHanded = ref(false)
    const isNumpadDisabled = ref(false)
    const minimumValue = ref('1')
    const maximumValue = ref('999')
    const formatter = ref('0,0.[0000]')
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

    const onNumpadConfirm = (event: Event) => alert(`Confirm event has been emitted ${event}`)

    const onCurrencyChange = (currencySign: string) => {
      alert(`Currency change event has been emitted with ${currencySign}`)
    }

    return {
      layout,
      formatter,
      isNumpadLeftHanded,
      isNumpadDisabled,
      areScreenAndOperatorsVisible,
      isRemoveButtonVisible,
      isCurrencyChangerVisible,
      minimumValue,
      maximumValue,
      onNumpadConfirm,
      onCurrencyChange
    }
  }
})
</script>
