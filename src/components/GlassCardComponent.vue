<template>
  <div
    class="group relative max-w-5xl backdrop-blur-xl border border-gray-700/50 rounded-3xl pt-8 px-8 transition-all duration-500 hover:border-gray-600/60 overflow-hidden max-h-[600px]"
    @mouseenter="handleButtonEnter"
    @mouseleave="handleButtonLeave"
  >
    <!-- Glass reflection effect -->
    <div
      class="absolute inset-0 bg-gradient-to-br from-white/5 via-transparent to-transparent pointer-events-none rounded-3xl"
    ></div>

    <!-- Animated border glow -->
    <div
      class="absolute inset-0 rounded-3xl opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"
    >
      <!-- <div
        class="absolute inset-0 rounded-3xl bg-gradient-to-r from-blue-500/20 via-purple-500/20 to-pink-500/20 blur-sm"
      ></div> -->
    </div>

    <div class="flex flex-col gap-10 relative z-10">
      <div class="flex flex-col gap-1">
        <h1 class="text-2xl font-medium text-white">Test Hub Text</h1>
        <p>
          <span class="text-white font-medium">Google, '22</span> — Envisioning a future of
          playtesting for all developers.
        </p>
      </div>

      <div class="relative">
        <div
          class="transform transition-transform duration-700 ease-out"
          :class="isHovered ? '-translate-y-4' : 'translate-y-0'"
        >
          <img
            :src="screenshot"
            alt="Test Hub Dashboard Screenshot"
            class="w-full h-auto object-cover"
          />
        </div>

        <!-- Subtle overlay gradient for better integration -->
        <div
          class="absolute inset-0 bg-gradient-to-t from-gray-900/10 via-transparent to-transparent pointer-events-none"
        ></div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, inject, type Ref } from 'vue'
import screenshot from '@/assets/images/screenshot.png'

const isHovered = ref(false)
const cursorState = inject('cursorState') as {
  cursorColor: Ref<string>
  cursorScale: Ref<string>
  cursorClass: Ref<string>
}

const handleButtonEnter = () => {
  isHovered.value = true
  cursorState.cursorColor.value = 'transparent'
  cursorState.cursorClass.value = ''
}

const handleButtonLeave = () => {
  isHovered.value = false
  cursorState.cursorColor.value = '#393939'
  cursorState.cursorClass.value = ''
}
</script>

<style scoped>
.group {
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
}

.group {
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
}

.group:hover {
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
}
</style>
