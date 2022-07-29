<template>
  <input type="text" v-model="query" @keyup.enter="setQuery" />
</template>

<script>
export default {
  name: "SearchInput",
  methods: {
    setQuery() {
      this.$emit("search", this.query);
    },
  },
  data() {
    return {
      query: "",
    };
  },
};
</script>

<style></style>
