<template>
  <div @mouseover="active" @mouseleave="!active" class="content-card">
    <div v-if="!show">
      <img :src="`https://image.tmdb.org/t/p/w500${info.poster_path}`" alt="" />
    </div>
    <div v-else>
      <p>
        {{ info.title }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: false,
    };
  },
  props: {
    info: Object,
  },

  methods: {
    active() {
      this.show = !this.show;
    },
  },
};
</script>

<style lang="scss" scoped>
.content-card {
  width: calc(100% / 4 - 30px);
  margin: 10px 15px;
  display: flex;
  flex-wrap: wrap;

  img {
    width: 100%;
    object-fit: cover;
  }
}
</style>

<!-- 
In FilmBox, le informazioni compariranno se:
@mouseover="show" 

bisogna creare un methods 
data() {
    return {
        active: false
    }
}

methods: {
    show: function() {
        this.active = !this.active
    }
}

TODO da implementare
 -->
