<template>
  <header class="header">
    <div class="header__content">
      <router-link to="/" class="header__title">Test Task</router-link>
    </div>
  </header>
</template>

<script setup lang="ts">
</script>

<style lang="scss" scoped>
@use "@/styles/_variables.scss" as *;

.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: $header-height;
  box-shadow: $header-shadow;
  background: $header-bg-color;
  z-index: 1;

  .header__content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    max-width: 1344px;
    padding: 0 $header-padding-x;
  }

  .header__title {
    font-size: 32px;
    font-weight: 700;
    color: $header-title-color;
    text-align: left;
    text-decoration: none;
  }
}

@media (max-width: 768px) {
  .header {
    height: $header-height-mobile;
    .header__content {
      padding: 0 24px;
    }
  }
}
</style>
