<template>
  <div class="content-card">
      {{info.title}}
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
    width: 300px;
    height: 400px;
    border: 1px solid black;
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
