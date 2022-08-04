<template>
  <div class="movies-list">
    <div class="content-movie-list">
      <MovieCards 
          v-for="movie in movies"
          :key="movie"
          :title="movie.display_title"
          :link="movie.link.url"
          :text="movie.summary_short"
          :image="movie.multimedia.src"
          :publishdate="movie.publication_date" />
   </div>
  </div>
</template>

<script>
 import MovieCards from "@/components/MovieCards.vue";

 export default {

  props: ['movies'],

  components: { MovieCards },
  
 };
</script>

<style></style>