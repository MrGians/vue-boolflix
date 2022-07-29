<template>
  <div class="card-cover">
    <!-- Card Cover -->
    <img class="cover" :src="`${imgUri}${item.poster_path}`" :alt="originalTitle" />

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
      <!-- Plot -->
      <!-- <div class="plot"></div> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "CardCover",
  props: {
    item: Object,
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
  },
  data() {
    return {
      imgUri: "https://image.tmdb.org/t/p/w342",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "./../assets/styles/style.scss";

.card-cover {
  width: 200px;
  color: $text-color;
  position: relative;

  .cover {
    transition: opacity 0.2s;
  }

  &:hover {
    .cover {
      opacity: 0;
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
    padding: 1rem;
    text-align: center;
    opacity: 0;

    .original-title {
      font-size: 0.8rem;
    }
    .vote {
      font-size: 0.8rem;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>
