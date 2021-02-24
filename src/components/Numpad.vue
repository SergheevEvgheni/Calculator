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
          :class="{
            'col-12': !areScreenAndOperatorsVisible,
            'order-2': isNumpadLeftHanded
          }"
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
                :disabled="isNumpadDisabled"
                button-type="number"
                value="7"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="8"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="9"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="4"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="5"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="6"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="1"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="2"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="3"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-8 flex-grow-1">
              <NumpadButton
                :disabled="isNumpadDisabled"
                button-type="number"
                value="0"
                @click="addZero"
              />
            </div>
            <div class="col-4">
              <NumpadButton
                v-if="!isRemoveButtonVisible"
                :disabled="isNumpadDisabled"
                button-type="number"
                value="."
                @btnClick="addDecSeparator"
              />
              <NumpadButton
                v-else
                :disabled="isNumpadDisabled"
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
            :disabled="isNumpadDisabled"
            :value="currencySign === '€' ? '€' : '$'"
            button-type="operator"
            @click="onCurrencyChange"
          />
          <NumpadButton
            :disabled="isNumpadDisabled"
            button-type="operator"
            value="+/-"
            @click="changeSign"
          />
          <NumpadButton
            :disabled="isNumpadDisabled"
            button-type="operator"
            @click="removeLastChar"
          >
            <i class="fas fa-backspace"/>
          </NumpadButton>
          <NumpadButton
            :disabled="isNumpadDisabled"
            button-type="operator"
            value="C"
            @click="clearNumpad"
          />
          <NumpadButton
            :disabled="isNumpadDisabled"
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
    isNumpadDisabled: {
      type: Boolean,
      required: true
    },
    areScreenAndOperatorsVisible: {
      type: Boolean,
      required: true
    },
    isRemoveButtonVisible: {
      type: Boolean,
      required: true
    },
    isCurrencyChangerVisible: {
      type: Boolean,
      required: true
    },
    minimumValue: {
      type: String,
      required: true
    },
    maximumValue: {
      type: String,
      required: true
    },
    formatter: {
      type: String,
      default: '0,0.[0000]'
    }
  },
  emits: ['confirm', 'currencyChange'],
  setup (props, { emit }) {
    const numpadValue = ref('')
    const currencySign = ref('€')

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
      if (numpadValue.value.length) {
        const isSeparatorLastCharacter = numpadValue.value.slice(-1) === '.'
        const displayedValue = isSeparatorLastCharacter ? numpadValue.value.slice(0, -1) : numpadValue.value

        const isInMaxRange = Number(numpadValue.value) <= Number(props.maximumValue)
        const isInMinRange = Number(numpadValue.value) >= Number(props.minimumValue)

        if (isInMaxRange && isInMinRange) {
          emit('confirm', displayedValue)
          clearNumpad()
        } else {
          alert('The number you dialed is not in the allowed range')
        }
      }
    }

    const onCurrencyChange = () => {
      emit('currencyChange', currencySign.value)
      currencySign.value = currencySign.value === '€' ? '$' : '€'
    }

    const formattedValue = computed(() => {
      console.log(numpadValue.value)

      return numeral(numpadValue.value).format(props.formatter)
    })

    const onKeyDown = (event: KeyboardEvent) => {
      if (props.isNumpadDisabled) return
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
      currencySign,
      clearNumpad,
      removeLastChar,
      addCharacter,
      addZero,
      addDecSeparator,
      changeSign,
      confirm,
      onKeyDown,
      onCurrencyChange
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
