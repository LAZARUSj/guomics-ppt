<template>
  <div class="slidev-layout guomics-outline">
    <img class="guomics-bg" src="/backgrounds/bg-3.jpg" alt="" />
    <h2 class="outline-title">Outline</h2>
    <div class="outline-list">
      <slot />
    </div>
    <LogoBar variant="white" set="pair" position="bottom-right" size="footer" />
  </div>
</template>

<style scoped>
.guomics-outline {
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

.outline-title {
  position: absolute;
  left: 36px;
  top: 282px;
  margin: 0;
  color: #005091;
  font-family: 'Arial Black', Arial, sans-serif;
  font-size: 40px;
  font-weight: 900;
}

.outline-list {
  position: absolute;
  top: 112px;
  left: 290px;
  width: 450px;
  color: #ffffff;
}

.outline-list :deep(ol),
.outline-list :deep(ul) {
  counter-reset: outline-item;
  margin: 0;
  padding: 0;
  list-style: none;
}

.outline-list :deep(li) {
  margin: 0 0 24px;
  color: #ffffff;
  font-family: 'Arial Black', Arial, sans-serif;
  font-size: 30px;
  font-weight: 900;
  line-height: 1.05;
}

.outline-list :deep(li::before) {
  counter-increment: outline-item;
  content: "• " counter(outline-item) ", ";
  color: #ffffff;
}
</style>
