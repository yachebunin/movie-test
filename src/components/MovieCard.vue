<template>
  <div class="movie-card">
    <img
      :src="movie.poster || defaultPoster"
      alt="Movie Poster"
      class="movie-card-poster"
      @error="onPosterError"
    />
    <div class="movie-card-title">{{ movie.name }}</div>
    <div class="movie-card-description">{{ movie.description }}</div>
    <div class="movie-card-labels">
      <MovieLabel
        v-for="(label, index) in labels"
        :key="index"
        :variant="label.variant"
        :icon="label.icon"
        :value="label.value"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import MovieLabel from './MovieLabel.vue';

interface Movie {
  id: number;
  name: string;
  description: string;
  duration: string;
  rating: number;
  poster?: string;
  genre: string;
}

const props = defineProps<{
  movie: Movie;
}>();

const defaultPoster =
  'https://i0.wp.com/www.henneth-annun.ru/wp-content/uploads/2014/10/hobbit3_poster0_horiz.jpg?ssl=1';

const onPosterError = (event: Event) => {
  const img = event.target as HTMLImageElement;
  img.src = defaultPoster;
};

const labels = computed(() => [
  {
    variant:
      props.movie.rating < 4 ? 'danger' : props.movie.rating < 7 ? 'warning' : 'success',
    icon: 'star.svg',
    value: props.movie.rating,
  },
  { variant: 'info', icon: 'video.svg', value: props.movie.genre },
  { variant: 'highlight', icon: 'clock.svg', value: props.movie.duration },
]);
</script>

<style lang="scss" scoped>
@use '@/styles/_variables' as *;

.movie-card {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 16px;
  background-color: $card-bg-color;
  border-radius: 16px;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  position: relative;

  &:hover {
    box-shadow: 8px 8px 0px 0px #702bfe;
    transform: translate(-8px, -8px);
  }

  .movie-card-poster {
    max-width: 100%;
    border-radius: 8px;
    background-color: $poster-bg-color;
    object-fit: cover;
  }

  .movie-card-title {
    font-size: 28px;
    font-weight: bold;
    color: $text-primary-color;
  }

  .movie-card-description {
    font-size: 14px;
    font-weight: 500;
    color: $text-secondary-color;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .movie-card-labels {
    display: flex;
    gap: 12px;
    margin-top: auto;
  }
}
</style>
