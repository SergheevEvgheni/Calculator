<template>
  <div class="container">
    <Numpad msg="Welcome to Your Vue.js + TypeScript App"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Numpad from './components/Numpad.vue'

export default defineComponent({
  name: 'App',
  components: {
    Numpad
  }
})
</script>

<style lang="scss">
  html {
    font-size: 62.5%;
    box-sizing: border-box;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  *,
  *::before,
  *::after {
    margin: 0;
    padding: 0;
    box-sizing: inherit;
  }
</style>
