<template>
  <header>
    <div class="container h-100">
      <div id="navbar" class="h-100">
        <h1>Boolflix</h1>
        <div class="search-box">
          <SearchInput @search="searchQuery" placeholder="Cerca Film o Serie" />
          <button class="custom-btn" type="button">Button</button>
        </div>
      </div>
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
@import "./../assets/styles/style.scss";

header {
  background-color: $primary-color;
  height: 50px;
}

#navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;

  h1 {
    text-transform: uppercase;
    color: $tertiary-color;
    margin: 0;
  }
  .search-box {
    display: flex;
    justify-content: center;
    align-items: center;

    .custom-btn {
      color: $text-color;
      background-color: $tertiary-color;
      border: none;
      border-radius: 0 5px 5px 0;
      transition: transform 0.1s;

      &:hover {
        transform: scale(1.05);
      }
    }
  }
}
</style>
