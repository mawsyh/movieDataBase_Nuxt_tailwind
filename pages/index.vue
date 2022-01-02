<template>
  <div>
    <HeaderNav />
    <div class="px-4 mx-auto 2xl:container">
      <SearchBox />
      <Loading v-if="loading" />
      <div v-else class="flex flex-wrap">
        <MovieCard v-for="movie in movies" :key="movie.id" :movie="movie" />
      </div>
      <NotFound v-if="movies.length === 0" />
    </div>
  </div>
</template>

<script>
import NotFound from "../components/NotFound.vue";
import Loading from "../components/Loading.vue";
import SearchBox from "../components/SearchBox.vue";
import MovieCard from "../components/MovieCard.vue";
import HeaderNav from "../components/HeaderNav.vue";
export default {
  components: { SearchBox, MovieCard, HeaderNav, Loading, NotFound },
  data() {
    return {
      movies: [],
      loading: false,
    };
  },
  async fetch() {
    if (this.$route.query.search) {
      await this.searched(this.$route.query.search);
    } else {
      await this.getMovies();
    }
  },
  methods: {
    async searched(value) {
      try {
        this.loading = true;
        const API = `https://api.themoviedb.org/3/search/movie?api_key=332a7824ec9def7b8fc06672df319a41&language=en-US&page=1&query=${value}`;
        var dataFromSearch = await this.$axios.$get(API);
      } catch (err) {
        console.log(err);
      } finally {
        this.loading = false;
        this.movies = dataFromSearch.results;
      }
    },
    async getMovies() {
      try {
        this.loading = true;
        const API =
          "https://api.themoviedb.org/3/movie/now_playing?api_key=332a7824ec9def7b8fc06672df319a41&language=en-US&page=1";
        var initialData = await this.$axios.$get(API);
      } catch (err) {
        console.log(err);
      } finally {
        this.loading = false;
        this.movies = initialData.results;
      }
    },
  },
  watch: {
    "$route.params.search": {
      handler: async function () {
        console.log(this.$route.query.search);
        if (this.$route.query.search === undefined) {
          return await this.getMovies();
        }
        await this.searched(this.$route.query.search);
      },
      deep: true,
    },
  },
  created() {
    this.$nuxt.$on("emitedFunction", async (searchedValue) => {
      await this.$router.push({ query: { search: searchedValue } });
    });
  },
  destroyed() {
    this.$nuxt.$off("emitedFunction");
  },
};
</script>
