<template>
  <div class="container">
    <div class="navbar">
      <h1>BOOLFLIX</h1>
      <ul>
        <li @click="$emit('homeFilter')">Home</li>
        <li @click="$emit('topSeriesTV')">Serie TV</li>
        <li @click="$emit('upComingFilm')">Film in arrivo</li>
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
  },
};
</script>

<style lang="scss" scoped>
@import "./style/header.scss";
</style>