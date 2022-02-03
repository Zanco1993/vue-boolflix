<template>
  <div class="content-card">
      <img :src="`https://image.tmdb.org/t/p/w500${info.poster_path}`" alt="">
  </div>

</template>

<script>
export default {
props: {
    info: Object
},
};
</script>

<style lang="scss" scoped>
.content-card {
    width: calc(100% / 4 - 30px);
    margin: 10px 15px;

    img{
        width: 100%;
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
