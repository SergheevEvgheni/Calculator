<template>
  <div class="numpad">
    <div class="numpad__header">
      <i class="fas fa-times" />
    </div>
    <div class="numpad__body">
      <div class="row">
        <div class="col-9 numpad__numbers">
          <div class="row">
            <div class="col-12">
              <input
                v-model="numpadValue"
                type="text"
                class="numpad__screen"
                placeholder="0"
              />
            </div>
          </div>

          <div class="row">
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="7"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="8"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="9"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="4"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="5"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="6"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="1"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="2"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="3"
                @btnClick="addCharacter"
              />
            </div>
            <div class="col-8 flex-grow-1">
              <NumpadBtn
                btn-style="number"
                value="0"
                @click="addZero"
              />
            </div>
            <div class="col-4">
              <NumpadBtn
                btn-style="number"
                value="."
                @btnClick="addCharacter"
              />
            </div>
          </div>
        </div>
        <div class="col-3 d-flex flex-column">
          <NumpadBtn
            btn-style="operator"
            value="+/-"
            @click="changeSign"
          />
          <NumpadBtn
            btn-style="operator"
            @click="removeLastChar"
          >
            <i class="fas fa-backspace"/>
          </NumpadBtn>
          <NumpadBtn
            btn-style="operator"
            value="C"
            @click="clearNumpad"
          />
          <NumpadBtn
            btn-style="check"
            @click="confirm"
          >
            <i class="fas fa-check"/>
          </NumpadBtn>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onBeforeUnmount } from 'vue'
import NumpadBtn from '@/components/NumpadBtn.vue'

export default defineComponent({
  name: 'Numpad',
  components: {
    NumpadBtn
  },
  setup () {
    const numpadValue = ref('')

    const addCharacter = (character: string) => {
      numpadValue.value += character
    }

    const clearNumpad = () => {
      numpadValue.value = ''
    }

    const removeLastChar = () => {
      numpadValue.value = numpadValue.value.slice(0, -1)
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
        alert(numpadValue.value)
        clearNumpad()
      }
    }

    const onKeyUp = (event: KeyboardEvent) => {
      const allowedCharacters = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '.'].includes(event.key)

      if (allowedCharacters) addCharacter(event.key)
      else if (event.key === 'Enter') confirm()
      else if (event.key === '0') addZero()
    }

    window.addEventListener('keyup', onKeyUp)

    onBeforeUnmount(() => {
      window.removeEventListener('keyup', onKeyUp)
    })

    return {
      numpadValue,
      clearNumpad,
      removeLastChar,
      addCharacter,
      addZero,
      changeSign,
      confirm
    }
  }
})
</script>

<style scoped lang="scss">
  .numpad {
    width: 380px;
    margin: 60px auto;
    box-shadow: 0 0 20px #424242;
    border-radius: 10px;
    &__header {
      background-color: #039AC3;
      height: 40px;
      text-align: right;
      padding: 12px;
      border-radius: 10px 10px 0 0;
      i {
        font-size: 18px;
        color: #fff;
        opacity: 0.6;
      }
    }
    &__body {
      padding: 20px 20px 10px 20px;
      border-radius: 0 0 10px 10px;
    }
    &__screen {
      text-align: right;
      padding: 5px 10px;
    }
    button, input {
      width: 100%;
      margin-bottom: 10px;
      font-size: 32px;
    }
  }
</style>
