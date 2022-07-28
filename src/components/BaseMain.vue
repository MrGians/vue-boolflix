<template>
  <main>
    <ol>
      <li v-for="movie in movies" :key="movie.id">
        Titolo: {{ movie.title }}, <br />
        Titolo Originale: {{ movie.original_title }}, <br />
        <div v-if="movie.original_language === 'it' || movie.original_language === 'en'">
          Lingua:
          <img
            width="20"
            :src="require(`./../assets/img/flags/${movie.original_language}.png`)"
            alt="Language Flag"
          />
        </div>
        <div v-else>Lingua: {{ movie.original_language }}, <br /></div>
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
