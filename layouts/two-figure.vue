<template>
  <div class="slidev-layout guomics-two-figure">
    <img class="guomics-bg" src="/backgrounds/bg-1.jpg" alt="" />
    <SubtitleBar>{{ $frontmatter.subtitle || 'Write here your subtitle' }}</SubtitleBar>
    <LogoBar variant="color" set="pair" position="top-right" size="content" />
    <div class="figures-container">
      <div class="figure-item">
        <slot name="left" />
      </div>
      <div class="figure-item">
        <slot name="right" />
      </div>
    </div>
    <div class="body-copy">
      <slot name="body" />
    </div>
    <div class="source-copy">
      <slot name="sources" />
    </div>
    <SlideNumber />
  </div>
</template>

<style scoped>
.guomics-two-figure {
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

.figures-container {
  position: absolute;
  top: 112px;
  left: 145px;
  right: 145px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 118px;
  align-items: start;
}

.figure-item {
  text-align: center;
  min-width: 0;
}

.figure-item :deep(img) {
  max-width: 100%;
  height: 220px;
  object-fit: contain;
}

.figure-item :deep(p) {
  margin: 8px 0 0;
  color: #000000;
  font-family: Arial, sans-serif;
  font-size: 18px;
  line-height: 1.15;
}

.body-copy {
  position: absolute;
  top: 395px;
  left: 105px;
  right: 95px;
}

.body-copy :deep(p) {
  margin: 0 0 20px;
  color: #000000;
  font-family: Arial, sans-serif;
  font-size: 21px;
  line-height: 1.14;
}

.body-copy :deep(strong) {
  font-family: 'Arial Black', Arial, sans-serif;
  font-weight: 900;
}

.source-copy {
  position: absolute;
  left: 96px;
  right: 92px;
  bottom: 12px;
  height: 18px;
  overflow: hidden;
}

.source-copy :deep(p) {
  margin: 0;
  color: #000000;
  font-family: Arial, sans-serif;
  font-size: 6.5px;
  line-height: 1.12;
  overflow-wrap: anywhere;
}

.source-copy :deep(a) {
  color: #000000;
  text-decoration: none;
}
</style>
