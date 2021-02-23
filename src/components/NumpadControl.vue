<template>
  <div class="row">
    <div class="col-6 offset-3 mt-5 card">
      <div class="card-body">
        <h1 class="card-title col-12 text-center">Numpad Control Panel</h1>
        <div class="row">

          <div class="col-4">
            <div class="row">
              <NumpadCheckbox
                :checked="isNumpadLeftHanded"
                label="Right Handed Mode"
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
              :view="view"
              @update:view="view = $event"
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
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, provide } from 'vue'
import Numpad from '@/components/Numpad.vue'
import NumpadCheckbox from '@/components/reusable/NumpadCheckbox.vue'
import NumpadSelect from '@/components/reusable/NumpadSelect.vue'

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
    const view = ref('Default')

    provide('isNumpadDisabled', isNumpadDisabled)

    return {
      isNumpadLeftHanded,
      isNumpadDisabled,
      view
    }
  }
})
</script>

<style scoped lang="scss">

</style>
