<template>
  <div>
    <label class="relative block my-8">
      <span class="sr-only">Search</span>
      <span class="absolute inset-y-0 left-0 flex items-center pl-2">
        <svg class="h-4 w-4" viewBox="0 0 40 40">
          <path
            d="M 21 3 C 11.621094 3 4 10.621094 4 20 C 4 29.378906 11.621094 37 21 37 C 24.710938 37 28.140625 35.804688 30.9375 33.78125 L 44.09375 46.90625 L 46.90625 44.09375 L 33.90625 31.0625 C 36.460938 28.085938 38 24.222656 38 20 C 38 10.621094 30.378906 3 21 3 Z M 21 5 C 29.296875 5 36 11.703125 36 20 C 36 28.296875 29.296875 35 21 35 C 12.703125 35 6 28.296875 6 20 C 6 11.703125 12.703125 5 21 5 Z"
          ></path>
        </svg>
      </span>
      <input
        class="placeholder:italic placeholder:text-gray-400 block bg-white border border-gray-300 rounded-md py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm"
        @keyup.enter="emitEvent"
        placeholder="Search for anything..."
        type="text"
        name="search"
        v-model.lazy="searchInput"
      />
    </label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchInput: "",
    };
  },
  methods: {
    emitEvent() {
      this.$nuxt.$emit("emitedFunction", this.searchInput);
    },
  },
  created() {
    this.searchInput = this.$route.query.search;
    this.$nuxt.$on("resetQuery", async () => {
      this.searchInput = "";
    });
  },
};
</script>
