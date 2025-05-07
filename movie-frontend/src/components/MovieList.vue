<template>
  <div class="row">
    <MovieCard v-for="movie in movies" :key="movie.id" :movie="movie" />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import MovieCard from "./MovieCard.vue";

const movies = ref([]);

const fetchMovies = async () => {
  try {
    const response = await axios.get("http://127.0.0.1:8000/api/movies/");
    movies.value = response.data;
  } catch (error) {
    console.error("Failed to fetch movies:", error);
  }
};

onMounted(fetchMovies);
</script>
