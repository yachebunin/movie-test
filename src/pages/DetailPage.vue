<template>
  <div class="detail-page">
    <div class="detail-page__content" v-if="movieData">
      <div class="detail-page__left">
        <div class="detail-page__subtitle">{{ movieData.name }}</div>
        <img
          class="detail-page__poster"
          :src="movieData.poster || defaultPoster"
          alt="Movie Poster"
        />
        <div class="detail-page__labels">
          <MovieLabel
            v-for="(label, index) in movieData.labels"
            :key="index"
            :variant="label.variant"
            :icon="label.icon"
            :value="label.value"
          />
        </div>
      </div>
      <div class="detail-page__right">
        <MovieInfo :description="movieData.description" />
        <TriviaInfo :trivia="movieData.trivia" />
        <ActorsInfo :actors="movieData.actors" />
      </div>
    </div>

    <div v-else>
      <p>No detailed data found for this movie.</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

import MovieLabel from '@/components/MovieLabel.vue';

import MovieInfo from '@/components/MovieInfo.vue';
import TriviaInfo from '@/components/TriviaInfo.vue';
import ActorsInfo from '@/components/ActorsInfo.vue';

interface Actor {
  name: string;
  imdb_id: string;
}

interface MovieDetail {
  id: number;
  name: string;
  description: string;
  duration: string;
  rating: number;
  poster: string | null;
  genre: string;
  trivia?: string[];
  actors?: Actor[];
  labels?: Array<{
    variant: string;
    icon: string;
    value: string | number;
  }>;
}

const route = useRoute();
const movieData = ref<MovieDetail | null>(null);

const defaultPoster =
  'https://i0.wp.com/www.henneth-annun.ru/wp-content/uploads/2014/10/hobbit3_poster0_horiz.jpg?ssl=1';

async function fetchMovieDetail() {
  try {
    const response = await fetch('/detail.json');
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    const items = data.items as MovieDetail[];

    const item = items.find(
      (m: MovieDetail) => m.id === Number(route.params.id)
    );

    if (item) {
      item.labels = [
        {
          variant:
            item.rating < 4 ? 'danger' : item.rating < 7 ? 'warning' : 'success',
          icon: 'star.svg',
          value: item.rating
        },
        {
          variant: 'info',
          icon: 'video.svg',
          value: item.genre
        },
        {
          variant: 'highlight',
          icon: 'clock.svg',
          value: item.duration
        }
      ];

      movieData.value = item;
    } else {
      movieData.value = null;
    }
  } catch (err) {
    console.error('Failed to fetch detail data:', err);
    movieData.value = null;
  }
}

onMounted(() => {
  fetchMovieDetail();
});
</script>

<style scoped lang="scss">
.detail-page {
  padding: 24px 46px;

  .detail-page__content {
    display: flex;
    gap: 64px;
  }

  .detail-page__subtitle{
    font-size: 32px;
    font-weight: 700;
    line-height: 37.5px;
    color: #fff;
  }

  .detail-page__left {
    display: flex;
    flex-direction: column;
    gap: 24px;
    width: 100%;
    max-width: 240px;
    position: sticky;
    top: 0;

    .detail-page__poster {
      height: 320px;
      object-fit: cover;
    }

    .detail-page__labels {
      display: flex;
      align-items: center;
      gap: 8px;
    }
  }

  .detail-page__right {
    display: flex;
    flex-direction: column;
    gap: 16px;
    width: 100%;
    max-width: 340px;
  }
}

@media (max-width: 768px) {
  .detail-page {
    padding: 16px 24px 60px;
    .detail-page__content {
      display: flex;
      flex-direction: column;
      gap: 64px;
    }

    .detail-page__left {
      width: 100%;
      max-width: 100%;
      position: relative;
      top: unset;

      .detail-page__poster {
        width: 100%;
        object-fit: cover;
      }
    }

    .detail-page__right {
      width: 100%;
      max-width: 100%;
    }
  }
}
</style>
