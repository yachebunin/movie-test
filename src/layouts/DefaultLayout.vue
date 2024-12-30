<template>
  <div class="default-layout">
    <Header />

    <main class="main-content">
      <router-view />
    </main>

    <Footer />
  </div>
</template>

<script setup lang="ts">
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
</script>

<style lang="scss" scoped>
@use "@/styles/_variables.scss" as *;

.default-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  padding-top: 100px;

  .main-content {
    flex: 1;
    display: flex;
    background: $layout-bg-color;
  }
}

@media (max-width: 768px) {
  .default-layout {
    padding-top: 60px;
  }
}
</style>