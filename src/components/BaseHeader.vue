<template>
  <header>
    <div id="navbar">
      <span>Boolflix</span>
      <input type="text" v-model="query" @keyup.enter="setQuery" />
    </div>
  </header>
</template>

<script>
export default {
  name: "BaseHeader",
  methods: {
    setQuery() {
      this.$emit("query-selection", this.query);
    },
  },
  data() {
    return {
      query: "",
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
