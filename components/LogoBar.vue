<template>
  <div class="logo-bar" :class="[`pos-${position}`, `size-${size}`, `align-${align}`]">
    <img
      v-for="logo in selectedLogos"
      :key="logo.src"
      :src="logo.src"
      :class="['logo-img', `logo-${logo.key}`]"
      :alt="logo.alt"
    />
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  variant: { type: String, default: 'color' },
  set: { type: String, default: 'full' },
  position: { type: String, default: 'top-right' },
  size: { type: String, default: 'content' },
  align: { type: String, default: 'center' },
  logos: { type: Array, default: null },
})

const LOGOS = {
  color: {
    full: [
      { key: 'westlake-university', alt: 'Westlake University', src: '/logos/westlake-university-color.png' },
      { key: 'westlake-lab', alt: 'Westlake Laboratory', src: '/logos/westlake-lab-color.png' },
      { key: 'guomics', alt: 'Guomics', src: '/logos/guomics-color.png' },
      { key: 'wecip', alt: 'WeCIP', src: '/logos/wecip-color.png' },
    ],
    pair: [
      { key: 'westlake-university', alt: 'Westlake University', src: '/logos/westlake-university-color.png' },
      { key: 'westlake-lab', alt: 'Westlake Laboratory', src: '/logos/westlake-lab-color.png' },
    ],
  },
  white: {
    full: [
      { key: 'westlake-university', alt: 'Westlake University', src: '/logos/westlake-university-white.png' },
      { key: 'westlake-lab', alt: 'Westlake Laboratory', src: '/logos/westlake-lab-white.png' },
      { key: 'guomics', alt: 'Guomics', src: '/logos/guomics-white.png' },
      { key: 'wecip', alt: 'WeCIP', src: '/logos/wecip-white.png' },
    ],
    pair: [
      { key: 'westlake-university', alt: 'Westlake University', src: '/logos/westlake-university-white.png' },
      { key: 'westlake-lab', alt: 'Westlake Laboratory', src: '/logos/westlake-lab-white.png' },
    ],
  },
}

const selectedLogos = computed(() => {
  if (props.logos?.length) {
    return props.logos.map((src, index) => ({ key: `custom-${index}`, alt: 'Logo', src }))
  }

  return LOGOS[props.variant]?.[props.set] || LOGOS.color.full
})
</script>

<style scoped>
.logo-bar {
  position: absolute;
  display: flex;
  align-items: center;
  gap: 12px;
  z-index: 10;
}

.align-center {
  justify-content: center;
}

.align-left {
  justify-content: flex-start;
}

.pos-top-center {
  top: 34px;
  left: 50%;
  transform: translateX(-50%);
}

.pos-top-right {
  top: 34px;
  right: 38px;
}

.pos-bottom-left {
  bottom: 24px;
  left: 26px;
}

.pos-bottom-right {
  right: 40px;
  bottom: 32px;
}

.logo-img {
  display: block;
  object-fit: contain;
}

.size-cover {
  gap: 18px;
}

.size-cover .logo-westlake-university { width: 146px; }
.size-cover .logo-westlake-lab { width: 168px; }
.size-cover .logo-guomics { width: 90px; }
.size-cover .logo-wecip { width: 138px; }

.size-content { gap: 8px; }
.size-content .logo-westlake-university { width: 41px; }
.size-content .logo-westlake-lab { width: 47px; }

.size-footer { gap: 9px; }
.size-footer .logo-westlake-university { width: 41px; }
.size-footer .logo-westlake-lab { width: 47px; }

.size-thanks {
  gap: 18px;
}

.size-thanks .logo-westlake-university { width: 146px; }
.size-thanks .logo-westlake-lab { width: 168px; }
.size-thanks .logo-guomics { width: 90px; }
.size-thanks .logo-wecip { width: 138px; }
</style>
