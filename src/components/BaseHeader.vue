<template>
  <header>
    <div id="navbar">
      <h1>Boolflix</h1>
      <SearchInput @search="searchQuery" />
    </div>
  </header>
</template>

<script>
import SearchInput from "./SearchInput.vue";
export default {
  name: "BaseHeader",
  components: { SearchInput },
  methods: {
    searchQuery(query) {
      this.$emit("search-query", query);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./assets/styles/style.scss";

header {
  /* Test Style */
  background-color: gray;
  height: 60px;
}
</style>
