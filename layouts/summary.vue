<template>
  <div class="slidev-layout guomics-summary">
    <img class="guomics-bg" src="/backgrounds/bg-2.jpg" alt="" />
    <div class="summary-content">
      <slot />
    </div>
    <LogoBar variant="white" set="pair" position="bottom-left" size="footer" />
  </div>
</template>

<style scoped>
.guomics-summary {
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

.summary-content {
  position: absolute;
  inset: 0;
}

.summary-content :deep(h1),
.summary-content :deep(h2) {
  position: absolute;
  top: 104px;
  left: 0;
  right: 0;
  margin: 0;
  color: #ff9300;
  text-align: center;
  font-family: 'Arial Black', Arial, sans-serif;
  font-size: 42px;
  font-weight: 900;
}

.summary-content :deep(ul) {
  position: absolute;
  top: 245px;
  left: 190px;
  right: 140px;
  margin: 0;
  padding-left: 28px;
  list-style: disc;
}

.summary-content :deep(li) {
  margin-bottom: 18px;
  color: #ffffff;
  font-family: Arial, sans-serif;
  font-size: 24px;
  line-height: 1.2;
}

.summary-content :deep(li::marker) {
  color: #ffffff;
}

.summary-content :deep(strong) {
  color: #ffffff;
  font-weight: 700;
}
</style>
