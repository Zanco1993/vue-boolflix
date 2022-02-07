<template>
  <div @mouseenter="over" @mouseleave="over" class="content-card">
    <div v-show="!active">
      <img
        v-if="serie.poster_path"
        :src="`https://image.tmdb.org/t/p/w500${serie.poster_path}`"
        alt=""
      />
      <div v-else>
        <img class="image-not-found" src="@/assets/not_image.png" alt="" />
      </div>
    </div>
    <div v-show="active">
      <p>
        <strong>Titolo Serie: </strong>
        <span v-if="serie.name === ''"> Not found </span>
        <span v-else>{{ serie.name }}</span>
      </p>

      <div>
        <strong>Lingua: </strong>
        <img
          class="flag"
          v-if="language.includes(serie.original_language)"
          :src="`/flag/${serie.original_language}.png`"
          alt=""
        />
        <span v-else>
          {{ serie.original_language }}
        </span>
      </div>

      <p>
        <strong>Voto: </strong>
        <span v-if="serie.vote_average === 0 || serie.vote_average === ''">
          Not found
        </span>

        <span v-else v-for="star in 5" :key="star">
          <i v-if="star <= countStars()" class="fas fa-star gold"></i>
          <i v-else class="fas fa-star"></i>
        </span>
      </p>

      <p>
        <strong>Overview: </strong>
        <span v-if="serie.overview === ''"> Not found </span>
        <span v-else>
          {{ serie.overview }}
        </span>
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
    serie: Object,
  },

  methods: {
    over() {
      this.active = !this.active;
    },

    countStars() {
      return Math.round(this.serie.vote_average / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./style/cardBox.scss";
</style>
