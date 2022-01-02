<template>
  <div
    class="flex flex-col text-white 2xl:w-3/12 lg:w-4/12 md:w-6/12 w-full px-2 mb-8 mx-auto"
  >
    <div class="relative">
      <img
        v-if="movie.poster_path"
        :src="`https://image.tmdb.org/t/p/original${movie.poster_path}`"
        alt=""
      />
      <img v-else src="~/assets/notfound.jpg" alt="" />
      <span class="absolute top-0 left-0 bg-red-700 p-2 rounded-br-xl">{{
        movie.vote_average
      }}</span>
    </div>
    <div class="flex justify-between gap-2 bg-red-700 text-white px-4 py-2">
      <div class="w-8/12 flex flex-col">
        <h4 class="font-bold text-lg truncate">
          {{ movie.title }}
        </h4>
        <p>Released: {{ movie.release_date }}</p>
      </div>

      <div class="w-4/12 m-auto text-center">
        <NuxtLink :to="`/movies/${movie.id}`">
          <button
            class="px-2 py-1 border-2 font-bold text-red-700 bg-white rounded hover:text-white hover:bg-red-700 transition duration-300 shadow-xl"
          >
            More Info
          </button>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["movie"],
  methods: {
    logger() {
      console.log(movie.poster_path);
    },
  },
};
</script>
