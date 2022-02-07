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
        <span v-if="serie.name === ''">
          Not found
        </span>
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
          <i v-if="star <= countStars()" class="fas fa-star"></i>
          <i v-else class="far fa-star"></i>
        </span>
      </p>

      <p>
        <strong>Overview: </strong>
        <span v-if="serie.overview === ''"> Not found </span>
        <span v-else>
          {{ serie.overview }}
        </span>
      </p>

       <div>
        <p class="more-info" @click="getInfo(serie)">Maggiori info </p>
        <p v-show="showGenres">
          <strong>Genere: </strong>
          <ul>
            <li
            v-show="showGenres"
            v-for="(genre, index) in listGenres"
            :key="index">
            {{ genre.name }}
            </li>
          </ul>
        </p>

        <p v-show="showGenres">
          <strong>Cast: </strong>
          <span v-for="(cast, index) in listCast" :key="index">
            <ul>
              <li v-if="index < 5">{{ cast.name }}</li>
            </ul>
          </span>
        </p>
      {{listGenres}}
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios";
// export default {
//   data() {
//     return {
//       active: false,
//       language: ["it", "en", "ja"],
//     };
//   },
//   props: {
//     serie: Object,
//   },

//   methods: {
//     over() {
//       this.active = !this.active;
//     },

//     countStars() {
//       return Math.round(this.serie.vote_average / 2);
//     },
//   },
// };
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
    serie: Object,
  },

  methods: {
    over() {
      this.active = !this.active;
    },

    countStars() {
      return Math.round(this.serie.vote_average / 2);
    },

    getInfo(serie) {
      axios
        .get(
          `https://api.themoviedb.org/3/discover/tv/${serie.id}?&api_key=0b9833208903abf98afe96ce83981542`
        )
        .then((res) => {
          this.listGenres = res.data.genres;
        });
      axios
        .get(
          `https://api.themoviedb.org/3/discover/tv/${serie.id}/credits?&api_key=0b9833208903abf98afe96ce83981542`
        )
        .then((res) => {
          this.listCast = res.data.cast;
        });
      // fai comparire o meno le informazioni richieste
      this.showGenres = !this.showGenres;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./style/cardBox.scss";
</style>
