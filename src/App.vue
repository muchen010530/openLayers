<template>
  <div id="app">
    <popup/>
  </div>
</template>

<script>
import popup from './components/popup.vue'

export default {
  name: 'app',
  components: {
    popup
    
  }
}
</script>

<style>
*{padding:0; margin:0;}
html,body{
  height: 100%;
}
#app {
  height: 100%;
}
</style>
