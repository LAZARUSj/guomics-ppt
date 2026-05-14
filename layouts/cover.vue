<template>
  <div class="slidev-layout guomics-cover">
    <img class="guomics-bg" src="/backgrounds/bg-1.jpg" alt="" />
    <LogoBar variant="color" set="full" position="top-center" size="cover" />
    <div class="cover-content">
      <slot />
    </div>
    <div class="cover-year">Guomics 2026</div>
  </div>
</template>

<style scoped>
.guomics-cover {
  position: relative;
  min-height: 100%;
  padding: 0;
  overflow: hidden;
  background: #ffffff;
}

.guomics-bg {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.cover-content {
  position: absolute;
  top: 238px;
  left: 64px;
  right: 64px;
  text-align: center;
  color: #000000;
}

.cover-content :deep(h1) {
  margin: 0 0 70px;
  font-family: 'Arial Black', Arial, sans-serif;
  font-size: 52px;
  font-weight: 900;
  line-height: 1.06;
  color: #000000;
  letter-spacing: 0;
  max-width: none;
  white-space: nowrap;
}

.cover-content :deep(p) {
  margin: 4px 0;
  font-family: Arial, sans-serif;
  font-size: 19px;
  line-height: 1.25;
  color: #000000;
}

.cover-content :deep(.presenter) {
  margin-bottom: 10px;
  font-size: 27px;
}

.cover-content :deep(.website) {
  position: absolute;
  top: 270px;
  left: 0;
  right: 0;
  margin: 0;
  font-family: 'Arial Black', Arial, sans-serif;
  font-size: 23px;
  font-weight: 900;
  color: #000000;
}

.cover-year {
  position: absolute;
  right: 14px;
  bottom: 15px;
  font-family: Arial, sans-serif;
  font-size: 12px;
  color: #ffffff;
}
</style>
