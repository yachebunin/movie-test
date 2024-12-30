<template>
    <div class="detail-page__block">
      <div class="detail-page__subtitle">Description</div>
      <div class="detail-page__description">
        {{ description }}
      </div>
    </div>
  </template>

  <script setup lang="ts">
  import { defineProps } from 'vue';

  const props = defineProps<{
    description: string;
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

  .detail-page__description {
    font-family: Roboto;
    font-size: 14px;
    font-weight: 500;
    line-height: 16.41px;
    color: #fff;
  }
  </style>