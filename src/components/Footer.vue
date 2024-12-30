<template>
  <footer class="footer">
    <div class="footer__content">
      <div class="footer__left">Test Task, 2022</div>
      <div class="footer__right">
        <a href="tel:5183632171" class="footer__number">518-363-2171</a>
        <div class="footer__address">91 Park St. Fairhope, AL 36532</div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
</script>

<style lang="scss" scoped>
@use "@/styles/_variables.scss" as *;

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  height: $footer-height;
  color: $footer-text-color;
  box-shadow: $footer-shadow;
  background: $footer-bg-color;
  z-index: 1;

  .footer__content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    max-width: 1344px;
    padding: 0 $footer-padding-x;
  }

  .footer__left {
    font-size: 18px;
    font-weight: 700;
    line-height: 21.09px;
    text-align: left;
  }

  .footer__right {
    display: flex;
    flex-direction: column;
    gap: 4px;
    font-size: 14px;
    font-weight: 500;
    line-height: 16.41px;
  }

  .footer__number {
    text-decoration-line: underline;
    text-decoration-style: solid;
    color: inherit;
  }
}

@media (max-width: 768px) {
  .footer {
    height: $footer-height-mobile;
    .footer__content {
      padding: 0 24px;
    }
  }
}
</style>
