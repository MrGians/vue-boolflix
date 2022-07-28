<template>
  <main>
    <!-- MOVIES -->
    <ol>
      <li><h3>MOVIES HERE</h3></li>
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
    <!-- TV SERIES -->
    <ol>
      <li><h3>TV SERIES HERE</h3></li>
      <li v-for="serie in series" :key="serie.id">
        Titolo: {{ serie.name }}, <br />
        Titolo Originale: {{ serie.original_name }}, <br />
        <div v-if="serie.original_language === 'it' || serie.original_language === 'en'">
          Lingua:
          <img
            width="20"
            :src="require(`./../assets/img/flags/${serie.original_language}.png`)"
            alt="Language Flag"
          />
        </div>
        <div v-else>Lingua: {{ serie.original_language }}, <br /></div>
        Voto: {{ serie.vote_average }} . <br />
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
    series: Array,
    query: String,
  },
};
</script>

<style>
main {
  display: flex;
}
ol {
  width: 50%;
}
</style>
