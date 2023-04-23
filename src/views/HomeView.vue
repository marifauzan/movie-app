<script>
import moment from 'moment';
import axios from 'axios';

export default {
  name: "Home",
  data() {
    return {
      movies: [],
    }
  },
  methods: {
    yearFormatDate: (date) => {
      return moment(date).format('YYYY');
    },
  },
  async mounted() {
    let result = await axios.get("http://api.tvmaze.com/search/shows?q=girls");
    console.log()
    this.movies = result.data;
  },
}
</script>

<template>
  <main class="h-screen w-screen overflow-hidden">
    <!-- Start: Header -->
    <section class="bg-white h-16 w-screen flex justify-between items-center">
      <div class="flex">
        <p class="mx-4 font-medium text-lg text-gray-500">Home</p>
        <p class="mx-4 font-medium text-lg text-gray-500">Browse</p>
        <p class="mx-4 font-medium text-lg text-gray-500">Movies</p>
        <p class="mx-4 font-medium text-lg text-gray-500">TV Shows</p>
        <p class="mx-4 font-medium text-lg text-gray-500">Watchlist</p>
        <p class="mx-4 font-medium text-lg text-gray-500">Genres</p>
      </div>
      <div class="flex">
        <div class="relative text-gray-400 focus-within:text-gray-400">
          <span class="absolute inset-y-0 left-0 flex items-center pl-2">
            <button type="submit" class="p-1 focus:outline-none focus:shadow-outline">
              <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                viewBox="0 0 24 24" class="w-6 h-6">
                <path d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
              </svg>
            </button>
          </span>
          <input type="input"
            class="py-2 p-12 text-black font-medium text-base rounded-md focus:bg-white focus:outline-gray-400"
            placeholder="Search..." autocomplete="off">
        </div>
        <div class="bg-black mx-4 w-10 h-10 rounded-full"></div>
      </div>
    </section>
    <!-- End: Header -->

    <!-- Start: Movie -->
    <section class="w-screen px-10 py-7">
      <h1 class="font-bold text-2xl">Popular Movie</h1>

      <div class="mt-3 flex flex-wrap">
        <div :key="movie.show.id" class="mr-10 my-5" v-for="movie in movies ">
          <img class="h-[240px] w-[160px] shadow-2xl rounded-lg" :src='movie.show.image.original' alt="" />
          <p class="mt-4 font-medium text-xl">{{ movie.show.name }}</p>
          <div class="flex justify-between">
            <p class="font-base text-sm">{{ yearFormatDate(movie.show.premiered) }}</p>
            <div class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="w-6 h-6 fill-yellow-300">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563 0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0 01-.84.61l-4.725-2.885a.563.563 0 00-.586 0L6.982 20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0 00-.182-.557l-4.204-3.602a.563.563 0 01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z" />
              </svg>
              <p class="ml-2 font-base text-sm">{{ movie.show.rating.average }}</p>
            </div>
          </div>
        </div>
      </div>

    </section>
    <!-- End: Movie -->
  </main>
</template>




