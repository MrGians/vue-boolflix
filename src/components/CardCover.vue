<template>
  <div class="card-cover">
    <!-- Card Cover -->
    <img class="cover" :src="cover()" :alt="originalTitle" />

    <!-- Card Information -->
    <div class="card-info">
      <!-- Main Title -->
      <h6 class="title">{{ title }}</h6>
      <!-- Original Title -->
      <span class="original-title">({{ originalTitle }})</span>
      <!-- Language -->
      <div class="language">
        <img
          v-if="hasLanguageFlag"
          :src="require(`./../assets/img/flags/${item.original_language}.png`)"
          :alt="item.original_language"
          width="35px"
        />
        <span v-else>{{ item.original_language }}</span>
      </div>
      <!-- Vote -->
      <div class="vote">
        <FaIcon v-for="n in voteRoundedUp" :key="n" icon="fa-solid fa-star" />
        <div v-if="voteRoundedUp !== 5">
          <FaIcon v-for="n in 5 - voteRoundedUp" :key="n" icon="fa-regular fa-star" />
        </div>
      </div>
      <!-- Genre -->
      <div class="genre">
        <div>Genere:</div>
        <span v-for="genre in genres" :key="genre.id">{{ genre.name }} </span>
      </div>
      <!-- Cast -->
      <div class="cast">
        <div>Cast:</div>
        <span v-for="credit in filteredCredits" :key="credit.id">{{ credit.original_name }} </span>
      </div>
      <!-- Overview -->
      <div class="overview"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CardCover",
  props: {
    item: Object,
    api: Object,
  },
  computed: {
    title() {
      return this.item.title || this.item.name;
    },
    originalTitle() {
      return this.item.original_title || this.item.original_name;
    },
    hasLanguageFlag() {
      const flags = ["it", "en"];
      return flags.includes(this.item.original_language);
    },
    voteRoundedUp() {
      let vote = this.item.vote_average;

      if (vote < 1) vote = 1;
      return Math.ceil(vote / 2);
    },
    filteredCredits() {
      return this.credits.slice(0, 5);
    },
  },
  methods: {
    cover() {
      if (!this.item.poster_path) return this.imgPlaceholder;
      return this.imgUri;
    },
    fetchAdditionalData() {
      let endpointType;
      if (this.item.title) endpointType = "movie";
      if (this.item.name) endpointType = "tv";

      const endpoint = `/${endpointType}/` + this.item.id;

      axios
        .get(
          `${this.api.baseUri}${endpoint}?api_key=b7dbfbbc8992a9c6e19724a411d702e7&language=it-IT&append_to_response=credits`
        )
        .then((res) => {
          this.credits = res.data.credits.cast;
          this.genres = res.data.genres;
        });
    },
  },
  data() {
    return {
      imgUri: "https://image.tmdb.org/t/p/w342" + this.item.poster_path,
      imgPlaceholder: "https://online-serije.com/img/noimage.jpg",
      credits: [],
      genres: [],
    };
  },
  created() {
    this.fetchAdditionalData();
  },
};
</script>

<style lang="scss" scoped>
@import "./../assets/styles/style.scss";

.card-cover {
  width: 100%;
  height: 100%;
  color: $text-color;
  position: relative;

  .cover {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: opacity 0.2s;
  }

  &:hover {
    .cover {
      opacity: 0.1;
    }
    .card-info {
      opacity: 1;
    }
  }

  .card-info {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 0.5rem;
    text-align: center;
    overflow: auto;
    opacity: 0;

    .original-title {
      font-size: 0.8rem;
    }
    .vote {
      font-size: 0.8rem;
      display: flex;
      justify-content: center;
      align-items: center;
      margin-top: 0.5rem;

      & > div {
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }
  }
}
</style>
