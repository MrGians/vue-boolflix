<template>
  <main>
    <div v-for="movie in movies" :key="movie.id">
      <CardCover :item="movie" />
    </div>
    <div v-for="serie in series" :key="serie.id">
      <CardCover :item="serie" />
    </div>
  </main>
</template>

<script>
import CardCover from "./CardCover.vue";
export default {
  name: "BaseMain",
  props: {
    movies: Array,
    series: Array,
  },
  components: { CardCover },
};
</script>

<style lang="scss" scoped>
@import "./../assets/styles/style.scss";
</style>
