<template>
  <div class="row">
    <div class="col-6 p-3 card mt-5 offset-3">
      <div class="card-body">
        <h1 class="card-title col-12 text-center">Numpad Control Panel</h1>
        <div class="col-4">
          <div class="row">
            <div class="form-check form-switch">
              <input
                v-model="isNumpadLeftHanded"
                class="form-check-input"
                type="checkbox"
                id="handMode"
              >
              <label class="form-check-label" for="handMode">Right Hand Mode</label>
            </div>
          </div>
          <div class="row">
            <div class="form-check form-switch">
              <input
                v-model="isNumpadDisabled"
                class="form-check-input"
                type="checkbox"
                id="is-disabled"
              >
              <label class="form-check-label" for="is-disabled">Is Numpad Disabled</label>
            </div>
          </div>
        </div>
        <div class="col-4"></div>
        <div class="col-4"></div>
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

export default defineComponent({
  name: 'NumpadWrapper',
  components: {
    Numpad
  },
  setup () {
    const isNumpadLeftHanded = ref(false)
    const isNumpadDisabled = ref(false)
    provide('isNumpadDisabled', isNumpadDisabled)
    return {
      isNumpadLeftHanded,
      isNumpadDisabled
    }
  }
})
</script>

<style scoped lang="scss">

</style>
