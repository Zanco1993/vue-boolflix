<template>
  <div id="app">
    <header-app @searchSeries="filterSeries" @searchMovies="filterMovies" />
    <main-container :films="filteredListMovies" :series="filteredListSeries"/>
  </div>
</template>

<script>
import HeaderApp from "./components/HeaderApp.vue";
import MainContainer from "./components/MainContainer.vue";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      popularMovies: [],
      listMovies: [],
      listSeries: [],
      filteredListMovies: [],
      filteredListSeries: []
    };
  },
  mounted() {
    axios
      .get(
        `https://api.themoviedb.org/3/movie/popular?&api_key=0b9833208903abf98afe96ce83981542`
      )
      .then((element) => {
        this.popularMovies = element.data.results;
        this.filteredListMovies = this.popularMovies;
      });
  },

  components: {
    HeaderApp,
    MainContainer,
  },

  methods: {
    filterMovies(inputMovies) {
      console.log("prova");
      if (inputMovies !== "") {
        axios
          .get(
            `https://api.themoviedb.org/3/search/movie?query=${inputMovies}&api_key=0b9833208903abf98afe96ce83981542`
          )
          .then((element) => {
            this.filteredListSeries = [];
            this.listMovies = element.data.results;
            this.filteredListMovies = this.listMovies;
          });
      }
    },
    filterSeries(inputSeries) {
      console.log("prova");
      if (inputSeries !== "") {
        axios
          .get(
            `https://api.themoviedb.org/3/search/tv?query=${inputSeries}&api_key=0b9833208903abf98afe96ce83981542`
          )
          .then((element) => {
            this.filteredListMovies = [];
            this.listSeries = element.data.results;
            this.filteredListSeries = this.listSeries;
          });
      }
    },
  },
};
</script>

<style lang="scss">
@import "./style/main.scss";
@import "~@fortawesome/fontawesome-free/css/all.css";
</style>
