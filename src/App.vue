<template>
  <HeaderSection />
  <FilterSection @fetch-movies="filtIt" />
  <PagesControll @page-control="fetchByPage" ></PagesControll>
  <!-- <LoadingSpinner v-if="loading" /> -->
  <!-- <h1 v-else-if="!loading && errors" class="text-center font-bold text-4xl my-12">Something went wrong - try again later!</h1> -->
  <movies-list :movies="moviesData" ></movies-list>
</template>

<script>
import HeaderSection from '@/components/HeaderSection.vue'
import FilterSection from '@/components/FilterSection.vue'
import MoviesList from '@/components/MoviesList.vue';
// import LoadingSpinner from '@/components/LoadingSpinner.vue';
import PagesControll from '@/components/PagesControll.vue';
import { API_KEY } from '@/apikey.js';

export default {
  components: {
    HeaderSection,
    FilterSection,
    MoviesList,
    // LoadingSpinner,
    PagesControll,
},
  data() {
    return {
      moviesData: [],
      // errors: null,
      // loading: false,
      offsetNum: 0,
      movieOrder: "by-opening-date",
      query: "",
    }
  },
  methods: {
    filtIt(movieOrder, search) {
      this.fetchMovies(this.offsetNum, movieOrder, search);
    },
    fetchByPage(offsetNum) {
      this.offsetNum = offsetNum;
      this.fetchMovies(this.offsetNum, this.movieOrder, this.query);
    },
    async fetchMovies(offsetNum = 0, movieOrder = "by-opening-date", query = "") {

            const response = await fetch(`https://api.nytimes.com/svc/movies/v2/reviews/picks.json?api-key=${API_KEY}&offset=${offsetNum}&order=${movieOrder}&query=${query}`);
         
                const data = await response.json();
                this.moviesData = data.results;
    }
  },
  async mounted() {
        document.title = "NYT Critic's Picks";
       await this.fetchMovies();
  }
}
</script>
