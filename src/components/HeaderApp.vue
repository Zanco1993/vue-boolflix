<template>
  <div class="container">
    <h1>BOOLFLIX</h1>

    <div class="content-filter">
      <input type="text" @keyup.enter="$emit('search', input)" v-model="input" />
      <button @click="$emit('search', input)">Cerca</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "./style/header.scss";
</style>