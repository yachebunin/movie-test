<template>
    <div class="detail-page__block" v-if="actors && actors.length">
      <div class="detail-page__subtitle">Actors</div>
      <div class="detail-page__actors">
        <ul>
          <li v-for="(actor, index) in actors" :key="index">
            <a :href="`https://www.imdb.com/name/${actor.imdb_id}`" target="_blank" rel="noopener noreferrer">
              {{ actor.name }}
            </a>
          </li>
        </ul>
      </div>
    </div>
  </template>

  <script setup lang="ts">
  import { defineProps } from 'vue';

  interface Actor {
    name: string;
    imdb_id: string;
  }

  const props = defineProps<{
    actors?: Actor[];
  }>();
  </script>

  <style scoped lang="scss">
  .detail-page__block {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .detail-page__subtitle {
    font-size: 32px;
    font-weight: 700;
    line-height: 37.5px;
    color: #fff;
  }

  .detail-page__actors {
    font-family: Roboto;
    font-size: 14px;
    font-weight: 500;
    line-height: 16.41px;
    color: #fff;

    ul {
      margin: 0;
      padding: 0 0 0 16px;

      a {
        font-family: Roboto;
        font-size: 14px;
        font-weight: 500;
        line-height: 16.41px;
        text-decoration: underline;
        color: #fff;
      }
    }
  }
  </style>
