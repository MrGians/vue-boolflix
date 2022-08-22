<template>
  <main>
    <div id="pagination">
      <!-- Movie Section -->
      <section id="movies">
        <!-- Section Title -->
        <h2>Movies List</h2>
        <!-- Movie Card List -->
        <div v-if="movies.length" class="row">
          <div v-for="movie in movies" :key="movie.id" class="col-4 p-1">
            <CardCover :item="movie" :api="api" />
          </div>
        </div>
        <div v-else>Non sono stati trovati risultati</div>
      </section>
      <!-- TV Series Section -->
      <section id="tv-series">
        <!-- Section Title -->
        <h2>TV Series List</h2>
        <!-- TV Series Card List -->
        <div v-if="series.length" class="row">
          <div v-for="serie in series" :key="serie.id" class="col-4 p-1">
            <CardCover :item="serie" :api="api" />
          </div>
        </div>
        <div v-else>Non sono stati trovati risultati</div>
      </section>
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
    api: Object,
  },
  components: { CardCover },
};
</script>

<style lang="scss" scoped>
@import "./../assets/styles/style.scss";

#pagination {
  display: flex;
  text-align: center;
  color: $text_color;

  #movies,
  #tv-series {
    flex-basis: 50%;
    padding: 0.5rem;

    h2 {
      margin: 1rem auto;
    }
    .row {
      margin: 0 auto;
    }
  }
}
</style>
