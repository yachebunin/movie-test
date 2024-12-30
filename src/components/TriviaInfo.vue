<template>
    <div class="detail-page__block" v-if="trivia && trivia.length">
      <div class="detail-page__subtitle">Trivia</div>
      <div class="detail-page__trivia">
        <ul>
          <li v-for="(item, index) in trivia" :key="index">{{ item }}</li>
        </ul>
      </div>
    </div>
  </template>

  <script setup lang="ts">
  import { defineProps } from 'vue';

  const props = defineProps<{
    trivia?: string[];
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

  .detail-page__trivia {
    font-family: Roboto;
    font-size: 14px;
    font-weight: 500;
    line-height: 16.41px;
    color: #fff;

    ul {
      margin: 0;
      padding: 0 0 0 16px;
    }
  }
  </style>
