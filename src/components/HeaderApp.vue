<template>
  <div class="container">
    <h1>BOOLFLIX</h1>

    <div class="content-filter">
      <div class="input-movies">

        <!-- prova reset campo input dopo aver cercato -->
        
        <input
          type="text"
          @keyup.enter="resetMoviesSearch(inputMovies)"
          v-model="inputMovies"
          placeholder="Digita Film"
        />
        <button @click="resetMoviesSearch(inputMovies)">Cerca Film</button>
      </div>
      <div>
        <input
          type="text"
          @keyup.enter="resetSeriesSearch(inputSeries)"
          v-model="inputSeries"
          placeholder="Digita Serie"
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
      inputSeries: ""
    };
  },

  methods: {
    resetMoviesSearch(inputMovies) {
      this.inputMovies = ''
      this.$emit('searchMovies', inputMovies)
    },

    resetSeriesSearch(inputSeries) {
      this.inputSeries = ''
      this.$emit('searchSeries', inputSeries)
    }
  }
};
</script>

<style lang="scss" scoped>
@import "./style/header.scss";
</style>