<script setup>
import { ref, onMounted } from "vue";

let movies = ref([]);

function fetchMovies() {
    fetch('/api/v1/movies')
        .then(response => response.json())
        .then(data => {
            movies.value = data.movies;
        })
        .catch(error => console.log(error));
}

onMounted(() => {
    fetchMovies();
});
</script>

<template>
    <div class="container mt-5">
        <h1 class="mb-4">Movies</h1>
        <div class="row">
            <div v-for="movie in movies" :key="movie.id" class="col-md-6 mb-4">
                <div class="card h-100 shadow-sm overflow-hidden">
                    <div class="row g-0 h-100">
                        <div class="col-md-4">
                            <img :src="movie.poster" class="img-fluid movie-poster" :alt="movie.title">
                        </div>
                        <div class="col-md-8">
                            <div class="card-body">
                                <h5 class="card-title fw-bold">{{ movie.title }}</h5>
                                <p class="card-text text-muted">{{ movie.description }}</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.movie-poster {
    width: 100%;
    height: 100%;
    object-fit: cover;
    min-height: 250px; 
}

.card {
    border: 1px solid #dee2e6;
    border-radius: 8px;
}
</style>