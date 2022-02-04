<template>
  <div @mouseenter="over" @mouseleave="over" class="content-card">
    <div v-show="!active">
      <img :src="`https://image.tmdb.org/t/p/w500${info.poster_path}`" alt="" />
    </div>
    <div v-show="active">
      <div>
        <strong>Titolo: </strong>
        <span>{{ info.title }}</span>
      </div>
      <div>
        <strong>Titolo Originale: </strong>
        <span>{{ info.original_title }}</span>
      </div>

      <div>
        <strong>Lingua: </strong>
        <!-- <img
          v-if="language.includes(info.original_language)"
          :src="`@/assets/${info.original_language}.jpg`"
          alt=""
        />
        <div v-else>
          {{ info.original_language }}
        </div> -->

        <!-- da rendere dinamica todo -->
        <img src="@/assets/en.png" alt="">
      </div>

      <div>
        <strong>Voto: </strong>
        <span>{{ info.vote_average }}</span>
      </div>
      <div>
        <strong>Overview: </strong>
        <span>{{ info.overview }}</span>
      </div>
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

    // flag() {
    //   this.language.forEach((element) => {
    //     if(element.includes(this.info.original_language)) {
    //       this.searchLang.push(this.info.original_language)
    //     } else {
    //       return this.info.original_language
    //     }
    //   });
    //   return `@/flag/${this.searchLang}.png`;

    // },
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
  }

  img {
    width: 100%;
    height: 400px;
    object-fit: cover;
  }
}
</style>
