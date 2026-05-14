<template>
  <div class="slidev-layout guomics-publications">
    <img class="guomics-bg" src="/backgrounds/bg-2.jpg" alt="" />
    <SubtitleBar dark :rule="false">{{ $frontmatter.subtitle || 'Write here your subtitle' }}</SubtitleBar>
    <div class="pub-grid">
      <slot />
    </div>
    <LogoBar variant="white" set="pair" position="bottom-left" size="footer" />
    <SlideNumber />
  </div>
</template>

<style scoped>
.guomics-publications {
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

.guomics-publications :deep(.subtitle-bar) {
  top: 42px;
  left: 103px;
  right: auto;
  width: 560px;
  font-size: 30px;
}

.pub-grid {
  position: absolute;
  top: 88px;
  left: 52px;
  right: 52px;
  display: grid;
  grid-template-columns: 1.12fr 1.12fr 1.12fr 1.42fr;
  gap: 16px 24px;
  align-items: start;
}

.pub-grid :deep(.pub-image) {
  height: 130px;
}

.pub-grid :deep(.pub-caption) {
  font-size: 12px;
}
</style>
