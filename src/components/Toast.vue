<!-- Toast.vue -->
<script setup>
defineProps({
  visible: {
    type: Boolean,
    default: false,
  },
  message: {
    type: String,
    default: ``,
  },
  type: {
    type: String,
    default: `success`, // success, error, warning
  },
})
</script>

<template>
  <Transition name="fade">
    <div v-if="visible" class="toast" :class="type">
      {{ message }}
    </div>
  </Transition>
</template>

<style scoped>
.toast {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  padding: 10px 20px;
  border-radius: 4px;
  color: white;
  font-size: 14px;
  z-index: 1000;
}

.success {
  background-color: #67c23a;
}

.error {
  background-color: #f56c6c;
}

.warning {
  background-color: #e6a23c;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
