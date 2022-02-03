<template>
  <div id="app">
    <header-app @search="filterFilm"/>
    <main-container :films="films" />
  </div>
</template>

<script>
import HeaderApp from "./components/HeaderApp.vue";
import MainContainer from "./components/MainContainer.vue"
import axios from 'axios'

export default {
  name: "App",
  data() {
    return {
      films: []
    }
  },

  components: {
    HeaderApp,
    MainContainer
  },

  methods: {
    filterFilm(input) {
      axios.get(`https://api.themoviedb.org/3/search/movie?query=${input}&api_key=0b9833208903abf98afe96ce83981542`).then((element) => {
        this.films = element.data.results
      })
    }
  }

};
</script>

<style lang="scss">
@import "./style/main.scss";
</style>
