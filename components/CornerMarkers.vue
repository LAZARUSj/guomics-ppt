<template>
  <div class="corner-markers">
    <div class="corner tl" :style="cornerStyle"></div>
    <div class="corner tr" :style="cornerStyle"></div>
    <div class="corner bl" :style="cornerStyle"></div>
    <div class="corner br" :style="cornerStyle"></div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  size: { type: Number, default: 12 },
  color: { type: String, default: '#FFFFFF' },
})

const cornerStyle = computed(() => ({
  width: props.size + 'px',
  height: props.size + 'px',
  background: props.color,
}))
</script>

<style scoped>
.corner-markers {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 2;
}
.corner {
  position: absolute;
}
.corner.tl { top: 0; left: 0; }
.corner.tr { top: 0; right: 0; }
.corner.bl { bottom: 0; left: 0; }
.corner.br { bottom: 0; right: 0; }
</style>
