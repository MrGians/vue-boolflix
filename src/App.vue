<template>
  <div>
    <BaseHeader @query-selection="displayMovies" />
    <BaseMain :movie-query="movieQuery" :movies="moviesList" />
  </div>
</template>

<script>
import axios from "axios";
import BaseHeader from "./components/BaseHeader.vue";
import BaseMain from "./components/BaseMain.vue";
export default {
  name: "App",
  components: { BaseHeader, BaseMain },
  data() {
    return {
      baseUri: "https://api.themoviedb.org/3",
      apiKey: "api_key=b7dbfbbc8992a9c6e19724a411d702e7",
      langIT: "language=it-IT",
      movieQuery: "",
      moviesList: [],
    };
  },
  methods: {
    fetchedMovies() {
      axios
        .get(`${this.baseUri}/search/movie?${this.apiKey}&${this.langIT}&query=${this.movieQuery}`)
        .then((res) => {
          this.moviesList = res.data.results;
        })
        .catch((err) => {
          console.log(err.message);
        });
    },
    displayMovies(value) {
      this.movieQuery = value;
      this.fetchedMovies();
    },
  },
};
</script>

<style lang="scss"></style>
