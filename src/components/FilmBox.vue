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
        <strong>Titolo Originale: </strong>
        <span>{{ info.original_title }}</span>
      </p>

      <div>
        <strong>Lingua: </strong>
        <img
          class="flag"
          v-if="language.includes(info.original_language)"
          :src="`/flag/${info.original_language}.png`"
          alt=""
        />
        <span v-else>
          {{ info.original_language }}
        </span>
      </div>

      <p>
        <strong>Voto: </strong>
        <span v-if="info.vote_average === 0 || info.vote_average === ''">
          Non trovato
        </span>

        <span v-else v-for="star in countStars()" :key="star">
          <i class="fas fa-star"></i>
        </span>
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
      language: ["it", "en", "ja"],
    };
  },
  props: {
    info: Object,
  },

  methods: {
    over() {
      this.active = !this.active;
    },

    countStars() {
      return Math.round(this.info.vote_average / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
.content-card {
  width: calc(100% / 4 - 30px);
  height: 400px;
  margin: 5px 15px;
  display: flex;
  flex-wrap: wrap;

  &:hover {
    background-color: black;
    color: white;
    padding: 40px 10px;
    overflow: auto;
    p {
      padding: 5px 0;
      font-size: 16px;
    }
    span {
      color: #7f7f7f;
    }

    .fa-star {
      color: yellow;
    }
  }

  img {
    width: 100%;
    height: 400px;
    object-fit: cover;
  }

  .flag {
    width: 30px;
    height: 20px;
  }
}
</style>
