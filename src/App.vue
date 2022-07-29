<template>
  <div>
    <!-- TODO CHANGE ALL -->
    <BaseHeader @search-query="startSearch" />
    <BaseMain :movies="moviesList" :series="tvSeriesList" />
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
      api: {
        baseUri: "https://api.themoviedb.org/3",
        api_key: "b7dbfbbc8992a9c6e19724a411d702e7",
        language: "language=it-IT",
      },
      moviesList: [],
      tvSeriesList: [],
    };
  },
  methods: {
    startSearch(query) {
      const { api_key, language } = this.api;
      const config = {
        params: {
          api_key,
          language,
          query,
        },
      };

      this.fetchData("/search/movie", "moviesList", config);
      this.fetchData("/search/tv", "tvSeriesList", config);
    },
    fetchData(endpoint, list, config) {
      axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
        this[list] = res.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
@import "./assets/styles/style.scss";
</style>
