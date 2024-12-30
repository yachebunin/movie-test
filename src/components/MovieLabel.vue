<template>
  <div class="movie-label" :class="variant">
    <img
      class="movie-label-icon"
      :src="resolvedIcon"
      alt="icon"
      @error="onIconError"
    />
    <span class="movie-label-value">{{ value }}</span>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps<{
  variant: 'success' | 'warning' | 'danger' | 'info' | 'highlight';
  icon: string;
  value: string | number;
}>();

const iconsMap: Record<string, string> = {
  'star.svg': new URL('@/assets/icons/star.svg', import.meta.url).href,
  'video.svg': new URL('@/assets/icons/video.svg', import.meta.url).href,
  'clock.svg': new URL('@/assets/icons/clock.svg', import.meta.url).href,
  'default-icon.svg': new URL('@/assets/icons/default-icon.svg', import.meta.url).href,
};

const resolvedIcon = computed(() => {
  return iconsMap[props.icon] || iconsMap['default-icon.svg'];
});

const onIconError = (event: Event) => {
  const img = event.target as HTMLImageElement;
  img.src = iconsMap['default-icon.svg'];
};
</script>

<style lang="scss" scoped>
@use '@/styles/_variables' as *;

.movie-label {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  padding: 2px 8px;
  border-radius: 8px;
  color: #fff;

  &.success {
    background-color: $success-color;
  }

  &.warning {
    background-color: $warning-color;
  }

  &.danger {
    background-color: $danger-color;
  }

  &.info {
    background-color: $info-color;
  }

  &.highlight {
    background-color: $highlight-color;
  }

  .movie-label-icon {
    width: 12px;
    height: 12px;
  }

  .movie-label-value {
    font-family: Roboto, sans-serif;
    font-size: 12px;
    font-weight: 500;
    line-height: 1.2;
  }
}
</style>
