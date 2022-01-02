<template>
  <div>
    <div
      class="flex flex-col lg:flex-row w-9/12 mx-auto justify-between pt-8 pb-4"
    >
      <img
        :src="`https://image.tmdb.org/t/p/original${movie.poster_path}`"
        class="lg:w-6/12"
        alt=""
      />
      <div class="lg:w-5/12 mt-8 text-white">
        <h1 class="font-bold text-2xl text-red-600 text-center">
          {{ movie.title }}
        </h1>
        <p class="text-lg text-center">
          {{ movie.tagline }}
        </p>
        <p class="mt-8">
          <span class="font-semibold">Release Date: </span>
          {{ movie.release_date }}
        </p>
        <p>
          <span class="font-semibold">Languages: |</span>
          <span
            v-for="language in movie.spoken_languages"
            :key="language.iso_639_1"
            >{{ language.english_name }} |
          </span>
        </p>
        <p>
          <span class="font-semibold">Score: </span> {{ movie.vote_average }}
        </p>
        <p><span class="font-semibold">Votes: </span> {{ movie.vote_count }}</p>
        <p>
          <span class="font-semibold">Genres: |</span>
          <span v-for="genre in movie.genres" :key="genre.id"
            >{{ genre.name }} |
          </span>
        </p>
        <p class="mt-4">
          <span class="font-semibold">Overview: </span>
          {{ movie.overview }}
        </p>

        <a @click="$router.back()">
          <button class="px-4 py-2 bg-red-700 text-white rounded my-8 ml-16">
            Back
          </button>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movie: {},
    };
  },
  async fetch() {
    await this.getMovie();
  },
  methods: {
    async getMovie() {
      try {
        const API = `https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=332a7824ec9def7b8fc06672df319a41&language=en-US`;
        const data = await this.$axios.$get(API);
        this.movie = data;
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style scoped></style>
