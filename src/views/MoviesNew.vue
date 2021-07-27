<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label for="title">Title:</label>
        <input id="title" type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label for="year">Year:</label>
        <input id="year" type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label for="plot">Plot:</label>
        <textarea id="plot" type="text" v-model="newMovieParams.plot"></textarea>
        <br />
        <label for="english">Is this movie in English? Check for yes</label>
        <input type="checkbox" id="english" v-model="newMovieParams.english" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      errors: [],
      newMovieParams: {},
    };
  },
  methods: {
    createMovie: function () {
      console.log("Creating a movie!");
      axios.post("/movies", this.newMovieParams).then((response) => {
        this.$router.push("/movies");
        console.log(response.data);
      });
    },
  },
};
</script>
