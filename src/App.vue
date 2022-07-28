<template>
  <div>
    <BaseHeader @query-selection="displayQueryResults" />
    <BaseMain :query="query" :movies="moviesList" :series="tvSeriesList" />
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
      query: "",
      moviesList: [],
      tvSeriesList: [],
    };
  },
  methods: {
    fetchedMovies() {
      axios
        .get(`${this.baseUri}/search/movie?${this.apiKey}&${this.langIT}&query=${this.query}`)
        .then((res) => {
          this.moviesList = res.data.results;
        });
    },
    fetchedTvSeries() {
      axios
        .get(`${this.baseUri}/search/tv?${this.apiKey}&${this.langIT}&query=${this.query}`)
        .then((res) => {
          this.tvSeriesList = res.data.results;
        });
    },
    displayQueryResults(value) {
      this.query = value;
      this.fetchedMovies();
      this.fetchedTvSeries();
    },
  },
};
</script>

<style lang="scss"></style>
