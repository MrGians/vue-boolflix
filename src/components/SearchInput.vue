<template>
  <div>
    <input v-model="query" @keyup.enter="setQuery" type="text" :placeholder="placeholder" />
  </div>
</template>

<script>
export default {
  name: "SearchInput",
  props: {
    placeholder: {
      type: String,
      default: "Cerca...",
    },
  },
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

<style lang="scss" scoped></style>
