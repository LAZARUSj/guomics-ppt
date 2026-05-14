<template>
  <div class="highlight-bar" :class="{ 'align-left': align === 'left' }" :style="{ background: color, color: textColor }">
    <slot />
  </div>
</template>

<script setup>
defineProps({
  color: { type: String, default: '#e8eef8' },
  textColor: { type: String, default: '#000000' },
  align: { type: String, default: 'center' },
})
</script>

<style scoped>
.highlight-bar {
  padding: 16px 24px;
  font-size: 22px;
  line-height: 1.36;
  text-align: center;
  z-index: 5;
}

.highlight-bar :deep(p) {
  margin: 6px 0;
}

.highlight-bar.align-left {
  text-align: left;
}
</style>
