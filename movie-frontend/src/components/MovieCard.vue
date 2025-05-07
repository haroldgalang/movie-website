<template>
  <div class="col-md-4 mb-4">
    <div class="card h-100">
      <img
        :src="movie.poster"
        class="card-img-top"
        alt="Poster"
        style="height: 300px; object-fit: cover"
      />
      <div class="card-body">
        <h5 class="card-title">{{ movie.title }}</h5>
        <p class="card-text">
          <strong>Genre:</strong> {{ movie.genre }}<br />
          <strong>Director:</strong> {{ movie.director }}<br />
          <strong>Year:</strong> {{ movie.release_year }}<br />
          <strong>Rating:</strong> {{ movie.rating }}
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  movie: Object,
});

const emit = defineEmits(["edit", "delete"]);

const handleEdit = () => {
  emit("edit", props.movie);
};

const handleDelete = () => {
  emit("delete", props.movie.id);
};
</script>
