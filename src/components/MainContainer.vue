<template>
  <div class="main-container">
    <film-box 
    v-for="(film, index) in films"
    :key="index"
    :info="film"
    />
    
  </div>
</template>

<script>
import FilmBox from "./FilmBox.vue";
export default {
  components: {
    FilmBox,
  },

  props: {
    films: Array,
  },
};
</script>

<style lang="scss" scoped>
.main-container {
  padding: 40px;
}
</style>

<!-- Il MainContainer dovrà richiamare un nuovo componente
che avrà le informazioni dei film.
Attraverso un v-for potremo ciclare tutti gli elementi che soddisfano il filtro

 -->

