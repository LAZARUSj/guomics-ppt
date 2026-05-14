<template>
  <div class="slidev-layout guomics-comparison">
    <img class="guomics-bg" src="/backgrounds/bg-1.jpg" alt="" />
    <SubtitleBar>{{ $frontmatter.subtitle || 'Write here your subtitle' }}</SubtitleBar>
    <LogoBar variant="color" set="pair" position="top-right" size="content" />
    <div class="comparison-container">
      <div class="comparison-item">
        <slot name="left" />
      </div>
      <div class="comparison-item">
        <slot name="right" />
      </div>
    </div>
    <HighlightBar class="comparison-highlight">
      <slot name="highlight" />
    </HighlightBar>
    <SlideNumber />
  </div>
</template>

<style scoped>
.guomics-comparison {
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

.comparison-container {
  position: absolute;
  top: 112px;
  left: 145px;
  right: 128px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 84px;
  align-items: start;
}

.comparison-item {
  min-width: 0;
  text-align: center;
}

.comparison-item :deep(img) {
  width: 100%;
  height: 250px;
  object-fit: contain;
}

.comparison-item :deep(p) {
  margin: 8px 0 0;
  color: #000000;
  font-family: Arial, sans-serif;
  font-size: 17px;
  line-height: 1.15;
}

.comparison-highlight {
  position: absolute;
  left: 153px;
  right: 150px;
  bottom: 18px;
}
</style>
