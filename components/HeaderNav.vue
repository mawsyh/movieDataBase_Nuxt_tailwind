<template>
  <div>
    <img
      class="md:h-80 h-64 w-full object-cover relative"
      src="~/assets/headerBackground.jpg"
      alt="background"
    />
    <div class="2xl:mx-auto 2xl:container px-4">
      <div
        class="absolute top-0 2xl:px-auto 2xl:container flex flex-col w-auto"
      >
        <span class="text-red-800 font-bold text-xs mt-16">NOW STREAMING</span>
        <span class="text-gray-200 text-4xl tracking-widest mt-4"
          ><span class="font-bold tracking-normal">Now</span> Streaming</span
        >

        <NuxtLink
          to="/"
          class="bg-white text-red-700 text-center w-36 py-2 px-4 rounded hover:bg-red-200 ease-in duration-200 mt-4 md:mt-16"
          ><button @click="deleteSearchInput" class="font-bold">
            Top Movies
          </button></NuxtLink
        >
      </div>
    </div>
  </div>
</template>

//
<script>
export default {
  methods: {
    deleteSearchInput() {
      this.$nuxt.$emit("resetQuery");
    },
  },
};
</script>
