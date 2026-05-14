<template>
  <div class="slidev-layout guomics-thanks">
    <img class="guomics-bg" src="/backgrounds/bg-2.jpg" alt="" />
    <LogoBar variant="white" set="full" position="top-center" size="thanks" />
    <div class="thanks-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.guomics-thanks {
  position: relative;
  min-height: 100%;
  padding: 0;
  overflow: hidden;
  background: #005091;
  color: #ffffff;
}

.guomics-bg {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.thanks-content {
  position: absolute;
  top: 170px;
  left: 80px;
  right: 80px;
  text-align: center;
}

.thanks-content :deep(h1) {
  margin: 0 0 88px;
  color: #ff9300;
  font-family: 'Arial Black', Arial, sans-serif;
  font-size: 88px;
  font-weight: 900;
  line-height: 1;
}

.thanks-content :deep(p) {
  margin: 6px 0;
  color: #ffffff;
  font-family: Arial, sans-serif;
  font-size: 19px;
  line-height: 1.25;
}

.thanks-content :deep(.presenter) {
  margin-bottom: 10px;
  font-size: 28px;
}

.thanks-content :deep(.website) {
  margin-top: 58px;
  color: #ff9300;
  font-family: 'Arial Black', Arial, sans-serif;
  font-size: 22px;
  font-weight: 900;
}
</style>
