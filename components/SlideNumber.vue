<template>
  <div class="slide-number" :class="[`pos-${position}`]" :style="{ color }">
    {{ $slidev.nav.currentPage }}
  </div>
</template>

<script setup>
defineProps({
  color: { type: String, default: '#FFFFFF' },
  position: { type: String, default: 'bottom-right' },
})
</script>

<style scoped>
.slide-number {
  position: absolute;
  font-size: 13px;
  font-family: 'Arial', sans-serif;
  z-index: 10;
}
.pos-bottom-right { bottom: 16px; right: 26px; }
.pos-bottom-left { bottom: 16px; left: 26px; }
</style>
