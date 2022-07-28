<template>
  <main>
    <ol>
      <li v-for="movie in movies" :key="movie.id">
        Titolo: {{ movie.title }}, <br />
        Titolo Originale: {{ movie.original_title }}, <br />
        Lingua: {{ movie.original_language }}, <br />
        Voto: {{ movie.vote_average }} . <br />
        <hr />
      </li>
    </ol>
  </main>
</template>

<script>
export default {
  name: "BaseMain",
  props: {
    movies: Array,
    movieQuery: String,
  },
};
</script>

<style></style>
