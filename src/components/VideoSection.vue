<template>
  <section class="py-20 bg-gradient-to-br from-slate-800 via-blue-800 to-slate-800 relative overflow-hidden">
    <!-- Background Pattern -->
    <div class="absolute inset-0 opacity-10">
      <div class="absolute inset-0 bg-gradient-to-r from-blue-600/20 to-purple-600/20"></div>
      <div class="absolute top-0 left-0 w-full h-full pattern-dots opacity-20"></div>
    </div>

    <div class="container mx-auto px-4 relative z-10">
      <!-- Section Header -->
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-bold text-white mb-6">
          See Our <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-purple-400">Vision</span> in Action
        </h2>
        <p class="text-xl text-gray-300 max-w-3xl mx-auto leading-relaxed">
          Experience the future of electric solutions through our innovative technology and sustainable approach
        </p>
      </div>

      <!-- Video Container -->
      <div class="max-w-6xl mx-auto">
        <div 
          class="relative group cursor-pointer rounded-2xl overflow-hidden shadow-2xl transform transition-all duration-500 hover:scale-105 hover:shadow-3xl"
          @mouseenter="playVideo"
          @mouseleave="pauseVideo"
        >
          <!-- Video Element -->
          <video
            ref="videoRef"
            class="w-full h-auto"
            muted
            loop
            preload="metadata"
            poster=""
          >
            <source src="/videos/video.mp4" type="video/mp4">
            Your browser does not support the video tag.
          </video>

          <!-- Overlay -->
          <div class="absolute inset-0 bg-gradient-to-t from-black/50 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>

          <!-- Play Button Overlay (shown when paused) -->
          <div 
            v-if="!isPlaying" 
            class="absolute inset-0 flex items-center justify-center bg-black/30 transition-all duration-300"
          >
            <div class="bg-white/20 backdrop-blur-sm rounded-full p-6 transform transition-all duration-300 group-hover:scale-110">
              <svg class="w-16 h-16 text-white" fill="currentColor" viewBox="0 0 24 24">
                <path d="M8 5v14l11-7z"/>
              </svg>
            </div>
          </div>

          <!-- Video Controls Info -->
          <div class="absolute bottom-4 left-4 right-4">
            <div class="bg-black/50 backdrop-blur-sm rounded-lg p-3 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
              <p class="text-white text-sm font-medium">
                Hover to play • {{ isPlaying ? 'Playing' : 'Paused' }}
              </p>
            </div>
          </div>
        </div>

        <!-- Video Description -->
        <div class="mt-8 text-center">
          <p class="text-gray-300 text-lg max-w-4xl mx-auto">
            Watch how we're revolutionizing the electric industry with cutting-edge technology, 
            sustainable practices, and innovative solutions that power the future.
          </p>
        </div>
      </div>
    </div>

    <!-- Decorative Elements -->
    <div class="absolute top-20 left-10 w-20 h-20 bg-blue-500/10 rounded-full blur-xl"></div>
    <div class="absolute bottom-20 right-10 w-32 h-32 bg-purple-500/10 rounded-full blur-xl"></div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const videoRef = ref(null)
const isPlaying = ref(false)

const playVideo = () => {
  if (videoRef.value) {
    videoRef.value.play()
    isPlaying.value = true
  }
}

const pauseVideo = () => {
  if (videoRef.value) {
    videoRef.value.pause()
    isPlaying.value = false
  }
}

// Handle video events
const handleVideoLoad = () => {
  if (videoRef.value) {
    videoRef.value.addEventListener('play', () => {
      isPlaying.value = true
    })
    videoRef.value.addEventListener('pause', () => {
      isPlaying.value = false
    })
    videoRef.value.addEventListener('ended', () => {
      isPlaying.value = false
    })
  }
}

onMounted(() => {
  handleVideoLoad()
})

onUnmounted(() => {
  if (videoRef.value) {
    videoRef.value.removeEventListener('play', () => {})
    videoRef.value.removeEventListener('pause', () => {})
    videoRef.value.removeEventListener('ended', () => {})
  }
})
</script>

<style scoped>
.shadow-3xl {
  box-shadow: 0 35px 60px -12px rgba(0, 0, 0, 0.5);
}

.pattern-dots {
  background-image: radial-gradient(circle, rgba(255, 255, 255, 0.1) 1px, transparent 1px);
  background-size: 60px 60px;
}

/* Custom scrollbar for webkit browsers */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 4px;
}

::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.3);
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.5);
}
</style>
