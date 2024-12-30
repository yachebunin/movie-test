<template>
  <div class="main-page">
    <div v-if="loading" class="loading">Loading movies...</div>
    <div v-else-if="error" class="error">{{ error }}</div>
    <div v-else class="movies-grid">
      <MovieCard
        v-for="movie in movies"
        :key="movie.id"
        :movie="movie"
        @click="goToDetail(movie.id)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import MovieCard from '@/components/MovieCard.vue';

interface Movie {
  id: number;
  name: string;
  description: string;
  duration: string;
  rating: number;
  poster: string;
  genre: string;
}

const movies = ref<Movie[]>([]);
const loading = ref(true);
const error = ref<string | null>(null);
const router = useRouter();

function goToDetail(id: number) {
  router.push({ path: `/movie/${id}` });
}

async function fetchMovies() {
  try {
    const response = await fetch('/movies.json');
    if (!response.ok) throw new Error(`HTTP Error: ${response.status}`);
    const data = await response.json();
    movies.value = data.items;
  } catch (err) {
    error.value = 'Failed to load movies. Please try again later.';
    console.error(err);
  } finally {
    loading.value = false;
  }
}

onMounted(() => {
  fetchMovies();
});
</script>

<style scoped lang="scss">
@use '@/styles/_variables' as *;

.main-page {
  max-width: 1344px;
  margin: 0 auto;
  padding: 32px 48px;

  .loading,
  .error {
    text-align: center;
    font-size: 1.5rem;
    color: $text-secondary-color;
    margin-top: 2rem;
  }
}

.movies-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
}

@media (max-width: 1440px) {
  .movies-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }
}

@media (max-width: 1024px) {
  .movies-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }
}

@media (max-width: 768px) {
  .main-page {
    padding: 16px 24px;
  }

  .movies-grid {
    display: grid;
    grid-template-columns: 100%;
    gap: 16px;
  }
}
</style>