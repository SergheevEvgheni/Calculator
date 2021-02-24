<template>
  <div
    class="numpad"
    tabindex="0"
    @keydown="onKeyDown"
  >
    <div class="numpad__header">
      <i class="fas fa-times" />
    </div>
    <div class="numpad__body">
      <div class="row">
        <div
          class="col-9 numpad__numbers"
          :class="{ 'order-2': isNumpadLeftHanded, 'col-12': !areScreenAndOperatorsVisible }"
        >
          <div
            v-if="areScreenAndOperatorsVisible"
            class="row"
          >
            <div class="col-12">
              <input
                :value="formattedValue"
                type="text"
                class="form-control numpad__screen"
                placeholder="0"
                disabled
                @input="numpadValue = $event.target.value"
              />
            </div>
          </div>

          <div class="row">
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="7"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="8"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="9"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="4"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="5"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="6"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="1"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="2"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                button-type="number"
                value="3"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-8 flex-grow-1">
              <NumpadButton
                button-type="number"
                value="0"
                @click="addZero"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                v-if="!isRemoveButtonVisible"
                button-type="number"
                value="."
                @btnClick="addDecSeparator"
              />
              <NumpadButton
                v-else
                button-type="operator"
                @click="removeLastChar"
              >
                <i class="fas fa-backspace"/>
              </NumpadButton>
            </div>
          </div>
        </div>
        <div
          v-if="areScreenAndOperatorsVisible"
          class="col-3 d-flex flex-column"
          :class="{ 'order-1' : isNumpadLeftHanded }"
        >
          <NumpadButton
            v-if="isCurrencyChangerVisible"
            button-type="operator"
          >
            $
          </NumpadButton>
          <NumpadButton
            button-type="operator"
            value="+/-"
            @click="changeSign"
          />
          <NumpadButton
            button-type="operator"
            @click="removeLastChar"
          >
            <i class="fas fa-backspace"/>
          </NumpadButton>
          <NumpadButton
            button-type="operator"
            value="C"
            @click="clearNumpad"
          />
          <NumpadButton
            button-type="check"
            @click="confirm"
          >
            <i class="fas fa-check"/>
          </NumpadButton>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue'
import NumpadButton from '@/components/interface/NumpadButton.vue'
import numeral from 'numeral'

export default defineComponent({
  name: 'Numpad',
  components: {
    NumpadButton
  },
  props: {
    isNumpadLeftHanded: {
      type: Boolean,
      required: true
    },
    layout: {
      type: String,
      required: true
    },
    layoutTypes: {
      type: Object,
      required: true
    },
    minimumValue: {
      type: String,
      required: true
    },
    maximumValue: {
      type: String,
      required: true
    }
  },
  emits: ['numpadValue'],
  setup (props, { emit }) {
    const numpadValue = ref('')

    const areScreenAndOperatorsVisible = computed(() => {
      const allowedLayouts = [props.layoutTypes.default, props.layoutTypes.currencyChanger]
      return allowedLayouts.includes(props.layout)
    })
    const isRemoveButtonVisible = computed(() => {
      return props.layout === props.layoutTypes.numbersRemove
    })
    const isCurrencyChangerVisible = computed(() => {
      return props.layout === props.layoutTypes.currencyChanger
    })

    const addCharacter = (character: string) => {
      numpadValue.value += character
    }

    const clearNumpad = () => {
      numpadValue.value = ''
    }

    const removeLastChar = () => {
      const slicedNumber = numpadValue.value.slice(0, -1)

      if (Number(slicedNumber)) {
        numpadValue.value = slicedNumber
      } else {
        clearNumpad()
      }
    }

    const addDecSeparator = () => {
      const separatorAlreadyExists = numpadValue.value.indexOf('.') === -1
      if (separatorAlreadyExists) addCharacter('.')
    }

    const addZero = () => {
      if (numpadValue.value.length) addCharacter('0')
    }

    const changeSign = () => {
      if (numpadValue.value.length) {
        const inverseNumber = Number(numpadValue.value) * -1
        numpadValue.value = String(inverseNumber)
      }
    }

    const confirm = () => {
      const isValueInAllowedRange = Number(numpadValue.value) >= Number(props.minimumValue) && Number(numpadValue.value) <= Number(props.maximumValue)
      if (numpadValue.value.length) {
        const isSeparatorLastCharacter = numpadValue.value.slice(-1) === '.'
        const displayedValue = isSeparatorLastCharacter ? numpadValue.value.slice(0, -1) : numpadValue.value

        alert(isValueInAllowedRange ? displayedValue : 'The number you dialed is not the allowed range')
        emit('numpadValue', numpadValue.value)
        clearNumpad()
      }
    }

    const formattedValue = computed(() => {
      return numeral(numpadValue.value).format('0,0.[0000]')
    })

    const onKeyDown = (event: KeyboardEvent) => {
      const allowedCharacters = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '.'].includes(event.key)

      if (allowedCharacters) addCharacter(event.key)
      else if (event.key === '0') addZero()
      else if (event.key === 'Backspace') removeLastChar()
      else if (event.key === 'Delete') addDecSeparator()
      else if (event.key === 'Enter') {
        event.stopPropagation()
        confirm()
      }
    }

    return {
      numpadValue,
      formattedValue,
      clearNumpad,
      removeLastChar,
      addCharacter,
      addZero,
      addDecSeparator,
      changeSign,
      confirm,
      areScreenAndOperatorsVisible,
      isRemoveButtonVisible,
      isCurrencyChangerVisible,
      onKeyDown
    }
  }
})
</script>

<style scoped lang="scss">
  .numpad {
    width: 38rem;
    margin: 0 auto;
    border-radius: 1rem;
    cursor: pointer;
    box-shadow: 0 0 1rem #424242;
    transition: all 0.2s;
    &:focus {
      box-shadow: 0 0 2rem #424242;
      outline: none;
    }
    &__header {
      background-color: #039AC3;
      border: 1px solid #039AC3;
      height: 4rem;
      text-align: right;
      padding: 1rem;
      border-radius: 1rem 1rem 0 0;
      i {
        font-size: 1.8rem;
        color: #fff;
        opacity: 0.6;
      }
    }
    &__body {
      padding: 2rem 2rem 1rem 2rem;
      border-radius: 0 0 1rem 1rem;
    }
    &__screen {
      text-align: right;
      padding: 0.5rem 1rem;
    }
    .btn, .form-control {
      width: 100%;
      margin-bottom: 1rem;
      font-size: 3.2rem;
    }
  }
</style>
