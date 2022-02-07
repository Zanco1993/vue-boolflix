<template>
  <div class="container">
    <div class="navbar">
      <h1>BOOLFLIX</h1>
      <ul>
        <li @click="homeFilter(inputSeries, inputMovies)">Home</li>
        <li @click="topSeriesTV(inputSeries, inputMovies)">Serie TV</li>
        <li @click="upComingFilm(inputSeries, inputMovies)">Film in arrivo</li>
      </ul>
    </div>

    <div class="content-filter">
      <div class="input-movies">
        <input
          type="text"
          @keyup.enter="resetMoviesSearch(inputMovies)"
          v-model="inputMovies"
          placeholder="Cerca Film"
        />
        <button @click="resetMoviesSearch(inputMovies)">Cerca Film</button>
      </div>
      <div>
        <input
          type="text"
          @keyup.enter="resetSeriesSearch(inputSeries)"
          v-model="inputSeries"
          placeholder="Cerca Serie"
        />
        <button @click="resetSeriesSearch(inputSeries)">Cerca Serie TV</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputMovies: "",
      inputSeries: "",
    };
  },

  methods: {
    resetMoviesSearch(inputMovies) {
      // se si vuole mantenere l'informazione della ricerca
      // basta commentare this.inputMovies

      // this.inputMovies = "";
      this.inputSeries = "";
      this.$emit("searchMovies", inputMovies);
    },

    resetSeriesSearch(inputSeries) {
      // se si vuole mantenere l'informazione della ricerca
      // basta commentare this.inputSeries

      // this.inputSeries = "";
      this.inputMovies = "";
      this.$emit("searchSeries", inputSeries);
    },
    homeFilter(inputSeries, inputMovies) {
      this.inputSeries = "";
      this.inputMovies = "";
      this.$emit("homeFilter", inputSeries, inputMovies);
    },
    topSeriesTV(inputSeries, inputMovies) {
      this.inputSeries = "";
      this.inputMovies = "";
      this.$emit("topSeriesTV", inputSeries, inputMovies);
    },
    upComingFilm(inputSeries, inputMovies) {
      this.inputSeries = "";
      this.inputMovies = "";
      this.$emit("upComingFilm", inputSeries, inputMovies);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./style/header.scss";
</style>