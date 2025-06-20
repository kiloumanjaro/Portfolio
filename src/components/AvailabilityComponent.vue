<template>
  <div class="flex items-center gap-3">
    <!-- Animated green circle with enhanced shadows -->
    <div class="relative">
      <!-- Outer glow ring -->
      <div
        class="absolute inset-0 rounded-full bg-green-400 opacity-30 animate-ping"
        :class="{ 'animate-ping': animated }"
      ></div>
      <!-- Main circle with enhanced shadows -->
      <div
        class="relative bg-gradient-to-br from-green-400 to-green-500 rounded-full shadow-lg shadow-green-500/25 drop-shadow-sm"
        :class="[
          sizeClasses,
          animated ? 'animate-pulse' : '',
          'ring-2 ring-green-300/20 ring-offset-1 ring-offset-white/10',
        ]"
      ></div>
    </div>

    <!-- Optional status text -->
    <span
      v-if="showText"
      class="text-sm text-gray-700 dark:text-gray-300 drop-shadow-sm"
      :class="textSizeClasses"
    >
      {{ statusText }}
    </span>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  size?: 'sm' | 'md' | 'lg' | 'xl'
  showText?: boolean
  statusText?: string
  animated?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  size: 'md',
  showText: true,
  statusText: 'Online',
  animated: true,
})

const sizeClasses = computed(() => {
  const sizes = {
    sm: 'w-2 h-2',
    md: 'w-3 h-3',
    lg: 'w-4 h-4',
    xl: 'w-5 h-5',
  }
  return sizes[props.size]
})

const textSizeClasses = computed(() => {
  const textSizes = {
    sm: 'text-xs',
    md: 'text-sm',
    lg: 'text-base',
    xl: 'text-lg',
  }
  return textSizes[props.size]
})
</script>

<style scoped>
/* Custom pulse animation for a more subtle effect */
@keyframes subtle-pulse {
  0%,
  100% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    opacity: 0.8;
    transform: scale(1.05);
  }
}

.animate-pulse {
  animation: subtle-pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>
