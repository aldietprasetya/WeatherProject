<template>
  <div id="app">
    <HelloWorld/>
  </div>
</template>
     
<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style lang="scss">
@import './assets/scss/style';
</style>
