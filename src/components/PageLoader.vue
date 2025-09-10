<template>
  <Transition name="fade-out">
    <div v-if="isLoading" class="fixed inset-0 z-50 bg-gradient-to-br from-slate-900 via-blue-900 to-slate-900 flex items-center justify-center">
      <div class="text-center">
        <!-- Logo -->
        <div class="mb-8">
          <h1 class="text-4xl font-bold text-white mb-2">
            <span class="text-electric-400">Ever</span>lectric
          </h1>
          <div class="w-32 h-1 bg-gradient-to-r from-electric-400 to-blue-400 mx-auto rounded-full"></div>
        </div>
        
        <!-- Loading Animation -->
        <div class="relative">
          <div class="w-16 h-16 border-4 border-electric-400/20 rounded-full animate-spin"></div>
          <div class="absolute top-0 left-0 w-16 h-16 border-4 border-transparent border-t-electric-400 rounded-full animate-spin"></div>
        </div>
        
        <!-- Loading Text -->
        <p class="text-gray-300 mt-6 animate-pulse">Loading your electric future...</p>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const isLoading = ref(true)

onMounted(() => {
  // Simulate loading time
  setTimeout(() => {
    isLoading.value = false
  }, 1500)
})
</script>

<style scoped>
.fade-out-enter-active,
.fade-out-leave-active {
  transition: opacity 0.5s ease;
}

.fade-out-enter-from,
.fade-out-leave-to {
  opacity: 0;
}
</style>

