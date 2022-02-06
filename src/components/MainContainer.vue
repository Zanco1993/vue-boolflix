<template>
  <div class="main-container">
    <div v-show="films !== ''" class="content">
      <film-box v-for="film in films" :key="film.id" :film="film" />
    </div>
    <div v-show="series !== ''" class="content">
      <serie-box v-for="serie in series" :key="serie.id" :serie="serie" />
    </div>
  </div>
</template>

<script>
import FilmBox from "./FilmBox.vue";
import SerieBox from "./SerieBox.vue";

export default {
  components: {
    FilmBox,
    SerieBox,
  },

  props: {
    films: Array,
    series: Array
  },
};
</script>

<style lang="scss" scoped>
.main-container {
  width: 1400px;
  margin: 0 auto;
  padding-top: 30px;

  .content {
    display: flex;
    flex-wrap: wrap;
  }
}
</style>



