<!-- ImageProcessingLoading.vue -->
<script setup>
import { computed } from 'vue'

const props = defineProps({
  isProcessing: {
    type: Boolean,
    default: false,
  },
  currentIndex: {
    type: Number,
    default: 0,
  },
  totalImages: {
    type: Number,
    default: 0,
  },
})

const progress = computed(() => {
  if (props.totalImages === 0)
    return 0
  return (props.currentIndex / props.totalImages) * 100
})
</script>

<template>
  <div v-if="isProcessing" class="loading-container">
    <div class="loading-content">
      <div class="spinner" />
      <div class="progress-text">
        正在处理图片 {{ currentIndex }}/{{ totalImages }}
      </div>
      <div class="progress-bar">
        <div
          class="progress-bar-inner"
          :style="{ width: `${progress}%` }"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.loading-container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
}

.loading-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  width: 300px;
  text-align: center;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #f3f3f3;
  border-top: 4px solid #0e88ebff;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto 15px;
}

.progress-text {
  margin-bottom: 10px;
}

.progress-bar {
  width: 100%;
  height: 6px;
  background: #f3f3f3;
  border-radius: 3px;
  overflow: hidden;
}

.progress-bar-inner {
  height: 100%;
  background: #0e88ebff;
  transition: width 0.3s ease;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
