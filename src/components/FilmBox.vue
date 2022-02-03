<template>
  <div @mouseenter="over" @mouseleave="over" class="content-card">
    <div v-show="!active">
      <img :src="`https://image.tmdb.org/t/p/w500${info.poster_path}`" alt="" />
    </div>
    <div v-show="active">
      <p>
        <strong>Titolo: </strong>
        <span>{{ info.title }}</span>
      </p>
      <p>
        <strong>Originale: </strong>
        <span>{{ info.original_title }}</span>
      </p>
      <p>
        <strong>Voto: </strong>
        <span>{{ info.vote_average }}</span>
      </p>
      <p>
        <strong>Overview: </strong>
        <span>{{ info.overview }}</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      active: false,
    };
  },
  props: {
    info: Object,
  },

  methods: {
    over() {
      this.active = !this.active;
    },
  },
};
</script>

<style lang="scss" scoped>
.content-card {
  width: calc(100% / 4 - 30px);
  margin: 5px 15px;
  display: flex;
  flex-wrap: wrap;

  &:hover {
    background-color: black;
    color: white;
    padding: 40px 10px;

    p {
      font-size: 16px;
    }
    span {
      color: #7f7f7f;
    }
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
