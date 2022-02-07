<template>
  <div @mouseenter="over" @mouseleave="over" class="content-card">
    <div v-show="!active">
      <img
        v-if="film.poster_path"
        :src="`https://image.tmdb.org/t/p/w500${film.poster_path}`"
        alt=""
      />
      <div v-else>
        <img class="image-not-found" src="@/assets/not_image.png" alt="" />
      </div>
    </div>

    <div v-show="active">
      <p>
        <strong>Titolo: </strong>
        <span v-if="film.title === '' || film.title === null"> Not found </span>
        <span v-else>{{ film.title }}</span>
      </p>

      <p>
        <strong>Titolo Originale: </strong>
        <span v-if="film.original_title === ''"> Not found </span>
        <span v-else>{{ film.original_title }}</span>
      </p>

      <div>
        <strong>Lingua: </strong>
        <img
          class="flag"
          v-if="language.includes(film.original_language)"
          :src="`/flag/${film.original_language}.png`"
          alt=""
        />
        <span v-else>
          {{ film.original_language }}
        </span>
      </div>

      <p>
        <strong>Voto: </strong>
        <span v-if="film.vote_average === 0 || film.vote_average === ''">
          Not found
        </span>

        <!-- gestione valutazione con stelline -->
        <span v-else v-for="star in 5" :key="star">
          <i v-if="star <= countStars()" class="fas fa-star gold"></i>
          <i v-else class="fas fa-star"></i>
        </span>
      </p>

      <p>
        <strong>Overview: </strong>
        <span v-if="film.overview === ''"> Not found </span>
        <span v-else>
          {{ film.overview }}
        </span>
      </p>

      <div>
        <p>
          <strong @click="getGenres(film)">Genere: </strong>
          <span v-show="showGenres" v-for="(genre, index) in listGenres" :key="index"
            >{{ genre.name }}
          </span>
        </p>

        <p>
          <strong @click="getCast(film)">Cast: </strong>
          <span v-for="(cast, index) in listCast" :key="index">
            <ul>
              <li v-if="index < 5">{{ cast.name }}</li>
            </ul>
          </span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      active: false,
      showGenres: false,
      language: ["it", "en", "ja"],
      listGenres: [],
      listCast: [],
    };
  },
  props: {
    film: Object,
  },

  methods: {
    over() {
      this.active = !this.active;
    },

    countStars() {
      return Math.round(this.film.vote_average / 2);
    },

    getGenres(film) {
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${film.id}?&api_key=0b9833208903abf98afe96ce83981542`
        )
        .then((res) => {
          this.listGenres = res.data.genres;
        });
      this.showGenres = !this.showGenres
    },
    getCast(film) {
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${film.id}/credits?&api_key=0b9833208903abf98afe96ce83981542`
        )
        .then((res) => {
          this.listCast = res.data.cast;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./style/cardBox.scss";
</style>
