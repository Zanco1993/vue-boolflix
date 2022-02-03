<template>
  <div id="app">
   <header-app/>

  </div>
</template>

<script>
import HeaderApp from './components/HeaderApp.vue'
// import axios from 'axios'

export default {
  name: 'App',
  components: {
    HeaderApp
  }
}
</script>

<style lang="scss">
@import './style/main.scss';
</style>
