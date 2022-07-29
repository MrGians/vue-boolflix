<template>
  <main>
    <!-- MOVIES -->
    <ol>
      <li><h3>MOVIES HERE</h3></li>
      <li v-for="movie in movies" :key="movie.id">
        Cover:
        <img :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`" alt="poster" /> <br />
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
        Voto: {{ voteRoundedUp(movie.vote_average) }} . <br />
        <hr />
      </li>
    </ol>
    <!-- TV SERIES -->
    <ol>
      <li><h3>TV SERIES HERE</h3></li>
      <li v-for="serie in series" :key="serie.id">
        Cover:
        <img :src="`https://image.tmdb.org/t/p/w342${serie.poster_path}`" alt="poster" /> <br />
        Titolo:
        {{ serie.name }}, <br />
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
        Voto: {{ voteRoundedUp(serie.vote_average) }} . <br />
        <FaIcon
          v-for="n in voteRoundedUp(serie.vote_average)"
          :key="n"
          :icon="['fa-solid', 'fa-star']"
        />
        <div v-if="voteRoundedUp(serie.vote_average) !== 5">
          <FaIcon
            v-for="n in 5 - voteRoundedUp(serie.vote_average)"
            :key="n"
            :icon="['fa-regular', 'fa-star']"
          />
        </div>
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
  methods: {
    voteRoundedUp(vote) {
      if (vote < 1) vote = 1;
      return Math.ceil(vote / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../assets/styles/style.scss";

main {
  display: flex;
}
ol {
  width: 50%;
}
</style>
