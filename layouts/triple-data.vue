<template>
  <div class="slidev-layout guomics-triple-data">
    <img class="guomics-bg" src="/backgrounds/bg-1.jpg" alt="" />
    <SubtitleBar>{{ $frontmatter.subtitle || 'Write here your subtitle' }}</SubtitleBar>
    <LogoBar variant="color" set="pair" position="top-right" size="content" />
    <div class="triple-container">
      <div class="triple-left">
        <slot name="left" />
      </div>
      <div class="triple-right">
        <div class="right-figure">
          <slot name="right-top" />
        </div>
        <div class="right-figure">
          <slot name="right-bottom" />
        </div>
      </div>
    </div>
    <HighlightBar class="triple-highlight" align="left">
      <slot name="highlight" />
    </HighlightBar>
    <SlideNumber />
  </div>
</template>

<style scoped>
.guomics-triple-data {
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

.triple-container {
  position: absolute;
  top: 105px;
  left: 116px;
  right: 116px;
  display: grid;
  grid-template-columns: 1.05fr 0.86fr;
  gap: 86px;
  align-items: start;
}

.triple-left {
  text-align: center;
}

.triple-left :deep(img) {
  width: 100%;
  height: 215px;
  object-fit: contain;
}

.triple-left :deep(p) {
  margin: 10px 0 0;
  color: #000000;
  font-family: Arial, sans-serif;
  font-size: 18px;
}

.triple-right {
  display: grid;
  grid-template-rows: 1fr 1fr;
  gap: 24px;
}

.right-figure :deep(img) {
  width: 100%;
  height: 180px;
  object-fit: contain;
}

.triple-highlight {
  position: absolute;
  left: 66px;
  bottom: 14px;
  width: 560px;
  font-size: 19px;
  line-height: 1.3;
}
</style>
