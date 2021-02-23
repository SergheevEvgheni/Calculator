<template>
  <div class="numpad">
    <div class="numpad__header">
      <i class="fas fa-times"></i>
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
                disabled
              />
            </div>
          </div>

          <div class="row">
            <div class="col-4">
              <button type="button" value="7" class="btn btn--number">7</button>
            </div>
            <div class="col-4">
              <button type="button" value="8" class="btn btn--number">8</button>
            </div>
            <div class="col-4">
              <button type="button" value="9" class="btn btn--number">9</button>
            </div>
            <div class="col-4">
              <button type="button" value="4" class="btn btn--number">4</button>
            </div>
            <div class="col-4">
              <button type="button" value="5" class="btn btn--number">5</button>
            </div>
            <div class="col-4">
              <button type="button" value="6" class="btn btn--number">6</button>
            </div>
            <div class="col-4">
              <button type="button" value="1" class="btn btn--number">1</button>
            </div>
            <div class="col-4">
              <button type="button" value="2" class="btn btn--number">2</button>
            </div>
            <div class="col-4">
              <button type="button" value="3" class="btn btn--number">3</button>
            </div>

            <div class="col-8 flex-grow-1">
              <button type="button" value="0" class="btn btn--number flex-grow-1">0</button>
            </div>
            <div class="col-4">
              <button type="button" class="btn btn--number" value=".">.</button>
            </div>
          </div>
        </div>

        <div class="col-3 d-flex flex-column numpad__control">
          <button type="button" class="btn btn--control">+/-</button>
          <button type="button" class="btn btn--control"><i class="fas fa-backspace"></i></button>
          <button type="button" class="btn btn--control">C</button>
          <button type="button" class="btn btn--control btn--check"><i class="fas fa-check"></i></button>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Numpad',
  props: {
    msg: String
  },
  setup (props) {
    console.log(props)
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
  }

  button, input {
    height: 60px;
    width: 100%;
    margin-bottom: 10px;
    font-size: 32px;
  }

  .btn {
    &--number {
      background-color: #424242;
      color: #fff;
      &:hover {
        color: #fff;
      }
    }
    &--control {
      background-color: #fff;
      color: #424242;
      border: 2px solid #424242;
    }
    &--check {
      flex: 1;
      background-color: #93D300;
      color: #fff;
      border: none;
      &:hover {
        color: #fff;
      }
    }
  }
</style>
