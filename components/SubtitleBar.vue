<template>
  <div class="subtitle-bar" :class="{ 'is-dark': dark, 'no-rule': !rule }">
    <slot />
  </div>
</template>

<script setup>
defineProps({
  dark: { type: Boolean, default: false },
  rule: { type: Boolean, default: true },
})
</script>

<style scoped>
.subtitle-bar {
  position: absolute;
  top: 42px;
  left: 102px;
  right: 58px;
  color: #000000;
  padding: 0 0 14px;
  border-bottom: 1px solid #222222;
  font-family: 'Arial Black', sans-serif;
  font-weight: 900;
  font-size: 30px;
  line-height: 1.1;
  z-index: 8;
}

.subtitle-bar.is-dark {
  color: #ffffff;
  border-bottom-color: transparent;
}

.subtitle-bar.no-rule {
  border-bottom: 0;
}
</style>
