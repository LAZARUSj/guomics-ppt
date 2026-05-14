<template>
  <div class="pub-card">
    <img :src="image" :alt="caption" class="pub-image" />
    <div class="pub-caption" v-if="caption">{{ caption }}</div>
  </div>
</template>

<script setup>
defineProps({
  image: { type: String, required: true },
  caption: { type: String, default: '' },
  href: { type: String, default: '' },
})
</script>

<style scoped>
.pub-card {
  min-width: 0;
  text-align: center;
}
.pub-image {
  width: 100%;
  height: 136px;
  object-fit: contain;
  background: #ffffff;
  border: 1px solid rgba(255, 255, 255, 0.55);
}
.pub-caption {
  padding: 8px 6px 0;
  font-size: 14px;
  line-height: 1.08;
  color: #FFFFFF;
  font-family: 'Arial', sans-serif;
}
</style>
