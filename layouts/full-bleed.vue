<template>
  <div class="slidev-layout guomics-full-bleed">
    <img class="guomics-bg" src="/backgrounds/bg-4.jpg" alt="" />
    <SubtitleBar dark :rule="false">{{ $frontmatter.subtitle || 'Write here your subtitle' }}</SubtitleBar>
    <div class="left-copy">
      <slot />
    </div>
    <div class="right-figure">
      <slot name="figure" />
    </div>
    <LogoBar variant="white" set="pair" position="bottom-left" size="footer" />
    <SlideNumber />
  </div>
</template>

<style scoped>
.guomics-full-bleed {
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

.guomics-full-bleed :deep(.subtitle-bar) {
  top: 78px;
  left: 70px;
  right: auto;
  width: 430px;
  font-size: 28px;
  line-height: 1.12;
  white-space: nowrap;
}

.left-copy {
  position: absolute;
  top: 170px;
  left: 88px;
  width: 390px;
}

.left-copy :deep(p) {
  margin: 0 0 18px;
  color: #ffffff;
  font-family: Arial, sans-serif;
  font-size: 20px;
  line-height: 1.16;
}

.left-copy :deep(.text-orange),
.left-copy :deep(strong) {
  color: #ff9300;
  font-weight: 700;
}

.right-figure {
  position: absolute;
  top: 38px;
  right: 40px;
  width: 370px;
  height: 480px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.right-figure :deep(p) {
  margin: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.right-figure :deep(img) {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}
</style>
