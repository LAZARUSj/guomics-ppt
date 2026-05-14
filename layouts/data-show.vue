<template>
  <div class="slidev-layout guomics-data-show">
    <img class="guomics-bg" src="/backgrounds/bg-1.jpg" alt="" />
    <SubtitleBar>{{ $frontmatter.subtitle || 'Write here your subtitle' }}</SubtitleBar>
    <LogoBar variant="color" set="pair" position="top-right" size="content" />
    <div class="data-container">
      <div class="data-left">
        <slot name="left" />
        <div v-if="$frontmatter.leftCaption" class="left-caption">
          {{ $frontmatter.leftCaption }}
        </div>
      </div>
      <div class="data-right">
        <slot name="right" />
      </div>
    </div>
    <HighlightBar class="data-highlight" align="left">
      <slot name="highlight" />
    </HighlightBar>
    <SlideNumber />
  </div>
</template>

<style scoped>
.guomics-data-show {
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

.data-container {
  position: absolute;
  top: 105px;
  left: 84px;
  right: 82px;
  display: grid;
  grid-template-columns: 45% 50%;
  gap: 40px;
  align-items: start;
}

.data-left {
  text-align: center;
}

.data-left :deep(img) {
  max-width: 235px;
  max-height: 190px;
  object-fit: contain;
}

.data-left :deep(p) {
  margin: 12px 0 0;
  color: #000000;
  font-family: Arial, sans-serif;
  font-size: 18px;
}

.left-caption {
  margin-top: 12px;
  color: #000000;
  font-family: Arial, sans-serif;
  font-size: 18px;
}

.data-right :deep(img) {
  width: 100%;
  height: 410px;
  object-fit: contain;
}

.data-highlight {
  position: absolute;
  left: 62px;
  bottom: 50px;
  width: 430px;
}
</style>
