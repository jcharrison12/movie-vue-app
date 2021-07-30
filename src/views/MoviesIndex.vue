<template>
  <div class="movies-index">
    Search for a movie
    <input v-model="filterText" />
    <div class="row" v-for="movie in filterBy(movies, filterText)" :key="movie.id">
      <div class="col-sm-6">
        <div class="card">
          <div class="card-body">
            <router-link v-bind:to="`/movies/${movie.id}`">
              <h5 class="card-title">{{ movie.title }}</h5>
            </router-link>
            <p class="card-text">{{ movie.year }}</p>
            <p class="card-text">{{ movie.plot }}</p>
            <!-- <a href="/movies/${movie.id}" class="btn btn-primary">More info</a> -->
          </div>
        </div>
      </div>
    </div>
    <!-- <div v-for="movie in movies" :key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <h1>{{ movie.title }}</h1>
      </router-link>
      <h2>{{ movie.year }}</h2>
      <p>{{ movie.plot }}</p>
      <p>English?: {{ movie.english }}</p>
    </div> -->
  </div>
</template>
<style></style>
<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      filterText: "",
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies:", this.movies);
      });
    },
  },
};
</script>
