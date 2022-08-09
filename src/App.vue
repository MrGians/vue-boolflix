<template>
  <div>
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
        credits: "append_to_response=credits",
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

      this.fetchData("/search/movie", "moviesList", config, "movie");

      this.fetchData("/search/tv", "tvSeriesList", config, "tv");
    },
    fetchData(endpoint, list, config, endpointType) {
      axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
        this[list] = res.data.results;

        // get more data from another API request and put the result in the main list
        this[list].forEach((item) => {
          // Config API
          const { api_key, language, credits } = this.api;
          const endpoint = `/${endpointType}/${item.id}`;

          axios
            .get(`${this.api.baseUri}${endpoint}?api_key=${api_key}&${language}&${credits}`)
            .then((res) => {
              // Push in each main-list element the corresponding necessary data from API result element
              item.credits = res.data.credits.cast;
              item.genres = res.data.genres;
            });
        });
      });
    },
  },
};
</script>

<style lang="scss">
@import "./assets/styles/style.scss";
</style>
