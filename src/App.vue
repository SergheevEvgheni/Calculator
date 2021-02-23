<template>
 <div class="container">
   <div class="row">
     <NumpadConfig />
   </div>
   <div class="row">
     <div class="col-9">
       <Numpad />
     </div>
     <div class="col-3">
       Numpad Logs
     </div>
   </div>
 </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import NumpadConfig from '@/components/NumpadConfig.vue'
import Numpad from '@/components/Numpad.vue'

export default defineComponent({
  name: 'App',
  components: {
    Numpad,
    NumpadConfig
  },
  setup () {
    console.log('setup')
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
