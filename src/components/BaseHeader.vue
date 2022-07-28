<template>
  <header>
    <div id="navbar">
      <span>Boolflix</span>
      <input type="text" v-model="movieQuery" @keyup.enter="setMovieQuery" />
    </div>
  </header>
</template>

<script>
export default {
  name: "BaseHeader",
  methods: {
    setMovieQuery() {
      this.$emit("query-selection", this.movieQuery);
    },
  },
  data() {
    return {
      movieQuery: "",
    };
  },
};
</script>

<style>
header {
  /* Test Style */
  background-color: gray;
  height: 60px;
}
</style>
