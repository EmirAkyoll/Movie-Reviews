<template>
  <div class="nav flex-center">

    <div class="search-nav flex-center">
      <div class="search-without-details"><img class="buyutec" src="@/images/buyutec.png" alt="buyutec resmi" />
      <input
        type="search"
        class="input-search"
        @change="filtIt" 
        name="search"
        v-model="search"
        placeholder="Search" /></div>
        <button @click="openWindow" class="search-button">Detailed Search</button>
    </div>
    
    <div class="sort-nav flex-center">
      <label class="sort-text" for="sortBy">Sort By: </label>
      <select
        class="sort-by-select"
        @change="filtIt"
        name="sortBy"
        id="sortBy"
        v-model="movieOrder">
        <option value="by-opening-date">Opening Date</option>
        <option value="by-publication-date">Publication Date</option>
      </select>
    </div>

  </div>
</template>

<script>
export default {
  components: {},
  emits: ['get-movies', 'open-window'],

  data() {
    return {
      search: "",
      movieOrder: "by-opening-date",
     
    };
  },
  
  methods: {

    openWindow(){ this.$emit("open-window", true); },

    filtIt(event) {
      const name = event.target.name;
      const value = event.target.value;

      if (name === "search") { this.search = value; }
      if (name === "sortBy") { this.movieOrder = value; }

      this.$emit("get-movies", this.movieOrder, this.search);
    },
  },
};
</script>

<style>
div.nav { justify-content: space-around; }

.sort-text {
  font-size: 16px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.sort-by-select {
  margin-left: 7px;
  font-size: 15.4px;
  padding: 8px;
  background-color: #f3f4f6;
  font-family: "Open Sans", sans-serif;
  border-radius: 6px;
  border: none;
  width: 155px;
}

.input-search {
  font-size: 15.6px;
  padding: 10px;
  border-radius: 8px;
  border: none;
  background-color: #f1f1f1;
  opacity: 0.8;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.sort-nav {
  border-radius: 18px;
  outline: none;
}

.buyutec {
  max-height: 18px;
  margin-right: 5px;
}

.search-button{
  width: 150px;
  height: 40px;
  margin-left: 25px;
  border: none;
  opacity: 0.8;
  border-radius: 5px;
  cursor: pointer;
}
.search-button:active{ background-color: #fff; }
</style>