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
                type="text"
                class="numpad__screen"
                placeholder="0"
              />
            </div>
          </div>

          <div class="row">
            <div class="col-4">
              <NumpadBtn btn-style="number">7</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">8</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">9</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">4</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">5</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">6</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">1</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">2</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">3</NumpadBtn>
            </div>
            <div class="col-8 flex-grow-1">
              <NumpadBtn btn-style="number">0</NumpadBtn>
            </div>
            <div class="col-4">
              <NumpadBtn btn-style="number">.</NumpadBtn>
            </div>
          </div>
        </div>

        <div class="col-3 d-flex flex-column">
          <NumpadBtn btn-style="operator">+/-</NumpadBtn>
          <NumpadBtn btn-style="operator"><i class="fas fa-backspace"/></NumpadBtn>
          <NumpadBtn btn-style="operator">C</NumpadBtn>
          <NumpadBtn btn-style="check"><i class="fas fa-check"/></NumpadBtn>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import NumpadBtn from '@/components/NumpadBtn.vue'

export default defineComponent({
  name: 'Numpad',
  components: {
    NumpadBtn
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
      direction: RTL;
      padding: 5px 10px;
    }
    button, input {
      width: 100%;
      margin-bottom: 10px;
      font-size: 32px;
    }
  }
</style>
