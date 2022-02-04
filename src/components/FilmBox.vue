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

        <!-- Non funziona -->

        <img
          class="flag"
          v-if="language.includes(info.original_language)"
          :src="`/flag/${info.original_language}.png`"
          alt=""
        />
        <div v-else>
          {{ info.original_language }}
        </div>

        <!-- da rendere dinamica todo -->
        <!-- <img src="@/assets/en.png" alt=""> -->
      </div>

      <p>
        <strong>Voto: </strong>
        <span v-if="info.vote_avarage === 0 || info.vote_avarage === ''">
          Non trovato
        </span>
        <span v-else v-for="(star, index) in 5" :key="index">
          
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
    height: 30px;
  }
}
</style>
