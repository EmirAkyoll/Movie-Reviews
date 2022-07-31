<template>
  <div class="container mx-auto mb-8">
    <div>
      <div class="nav flex-center">
        <div class="flex items-center p-4 space-x-2">
          <span class="fa fa-search"></span>
          <input
            type="search"
            name="search"
            id="search"
            placeholder="Search"
            class="bg-gray-100 p-2 rounded-md"
            @change="filter"
            v-model.trim="search"
          />
        </div>
        <div class="flex items-center p-4 space-x-2">
          <label for="sortBy">Sort By: </label>
          <select
            name="sortBy"
            id="sortBy"
            v-model="movieOrder"
            @change="filter"
            class="rounded-md bg-gray-100 p-2 cursor-pointer">

            <option value="by-opening-date">Opening Date</option>
            <option value="by-publication-date">Publication Date</option>
            <option value="by-title">Title</option>

          </select>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  emits: ["fetch-movies"],
  data() {
    return {
      search: "",
      movieOrder: "by-opening-date",
    };
  },
  methods: {
    filter(event) {
      const name = event.target.name;
      const value = event.target.value;
      if (name === "search") {
        this.search = value;
      }
      if (name === "sortBy") {
        this.movieOrder = value;
      }

      this.$emit("fetch-movies", this.movieOrder, this.search);
    },
  },
};
</script>

<style>
div.nav {
  justify-content: space-around;
}

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
</style>