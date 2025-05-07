<template>
  <div class="container mt-4">
    <h1 class="mb-4">My Movie Collection</h1>
    <MovieForm :onMovieAdded="fetchMovies" />
    <MovieList />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import axios from "axios";
import MovieList from "./components/MovieList.vue";
import MovieForm from "./components/MovieForm.vue";
import SearchBar from "./components/SearchBar.vue";

const movies = ref([]);
const searchTerm = ref("");

const fetchMovies = async () => {
  const res = await axios.get("http://127.0.0.1:8000/api/movies/");
  movies.value = res.data;
};

const handleSearch = (term) => {
  searchTerm.value = term;
};

const filteredMovies = computed(() =>
  movies.value.filter(
    (movie) =>
      movie.title.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      movie.genre.toLowerCase().includes(searchTerm.value.toLowerCase())
  )
);

onMounted(fetchMovies);
</script>
