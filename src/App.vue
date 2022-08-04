<template>
  <div>
     <DetailedSearch
        @send-selections="detailedSearch = $event; getMoviesWithDetails()"
        @is-this-excellent="criticPicks = $event"
        @close-window="withDetail = $event"
        v-show="withDetail">
     </DetailedSearch>

    <div :class="{ makeBlur: withDetail }">
     <HeaderSection></HeaderSection>
     <FilterSection 
        @open-window="withDetail = $event" 
        @get-movies="filtIt">
     </FilterSection>
      <!-- {{ detailedSearch }} -->
     <PageTransition 
        v-if="!withDetail"
        @page-transition="getPageWithNum">
     </PageTransition>
     <MoviesSection :movies="moviesData"></MoviesSection>
    </div>
  </div>
</template>

<script>
import HeaderSection from "@/components/HeaderSection.vue";
import FilterSection from "@/components/FilterSection.vue";
import PageTransition from "@/components/PageTransition.vue";
import MoviesSection from "@/components/MoviesSection.vue";
import DetailedSearch from "@/components/DetailedSearch.vue";
import { API_KEY } from "@/apikey.js";

export default {
  data() {
    return {
      moviesData: [],
      offsetNum: 0,
      movieOrder: "by-opening-date",
      query: "",
      withDetail: "",
      detailedSearch: null,
      criticPicks: "",
      reviewer: "",
    };
  },

  components: {
    HeaderSection,
    FilterSection,
    MoviesSection,
    PageTransition,
    DetailedSearch,
  },

  methods: {
    filtIt(movieOrder, search) {
      this.getMovies(this.offsetNum, movieOrder, search);
    },

    getPageWithNum(offsetNum) {
      this.offsetNum = offsetNum;
      this.getMovies(this.offsetNum, this.movieOrder, this.query);
    },

    async getMovies(offsetNum = 0, movieOrder = "by-opening-date", query = "") {
      const response = await fetch(
        `https://api.nytimes.com/svc/movies/v2/reviews/picks.json?api-key=${API_KEY}&offset=${offsetNum}&order=${movieOrder}&query=${query}`
      );

      const data = await response.json();
      this.moviesData = data.results;
    },

    async getMoviesWithDetails( criticPicks = this.detailedSearch.isThisExcellent,
                                offsetNum = (this.detailedSearch.pageNumber*20-20),
                                movieOrder = this.detailedSearch.listingSelection,
                                reviewer = this.detailedSearch.theReviewer,
                                query = this.detailedSearch.keyWord 
                                ){
      const response = await fetch(
        `https://api.nytimes.com/svc/movies/v2/reviews/picks.json?api-key=${API_KEY}&critics_pick=${criticPicks}&offset=${offsetNum}&query=${query}&order=${movieOrder}&reviewers=${reviewer}`
      );

      const data = await response.json();
      this.moviesData = data.results;
    },

    // async getReviewers(reviewers) {

    //   const response = await fetch(`https://api.nytimes.com/svc/movies/v2/reviews/picks.json?api-key=${API_KEY}&reviewers=${reviewers}`);

    //   const reviewer = await response.json();
    //   this.reviewers = reviewer.results;
    // },
  },

  async mounted() {
    document.title = "NYT Critic's Picks";
    await this.getMovies();
    // await this.getMoviesWithDetails();
    // await this.getReviewers();
  },
};
</script>

<style>
.makeBlur {
  filter: blur(2px);
  transition: all 0.2s;
}
</style>