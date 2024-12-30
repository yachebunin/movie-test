<template>
  <div class="app">
    <transition name="fade" mode="out-in">
      <router-view />
    </transition>
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped lang="scss">
@use '@/styles/_variables' as *;

$fade-duration: 0.3s;

.fade-enter-active, .fade-leave-active {
  transition: opacity $fade-duration ease-in-out;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>