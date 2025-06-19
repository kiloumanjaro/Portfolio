<template>
  <div class="relative overflow-hidden rounded-lg" :class="border">
    <video
      v-if="videoSrc"
      :src="videoSrc"
      class="w-full h-full object-cover"
      :controls="showControls"
      :autoplay="autoplay"
      :muted="muted"
      :loop="loop"
    ></video>
    <div v-else class="w-full h-full bg-gray-800 flex items-center justify-center">
      <div class="text-gray-400 text-center">
        <v-icon icon="mdi-video-outline" />
        <p class="text-sm">Video Placeholder</p>
      </div>
    </div>

    <div v-if="topLeftText" class="absolute top-4 left-4 text-[#171717] text-[13px] drop-shadow-lg">
      {{ topLeftText }}
    </div>

    <div
      v-if="topRightText"
      class="absolute top-4 right-4 text-black/55 text-[13px] drop-shadow-lg"
    >
      {{ topRightText }}
    </div>

    <div
      v-if="bottomLeftText"
      class="absolute bottom-4 left-4 text-[#171717] text-[13px] drop-shadow-lg"
    >
      {{ bottomLeftText }}
    </div>

    <div
      v-if="bottomRightText"
      class="absolute bottom-4 right-4 text-black/55 text-[13px] drop-shadow-lg"
    >
      {{ bottomRightText }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = withDefaults(
  defineProps<{
    videoSrc?: string
    showControls?: boolean
    autoplay?: boolean
    muted?: boolean
    loop?: boolean
    topLeftText?: string
    topRightText?: string
    bottomLeftText?: string
    bottomRightText?: string
    border?: string
  }>(),
  {
    videoSrc: '',
    showControls: false,
    autoplay: true,
    muted: true,
    loop: true,
    topLeftText: '',
    topRightText: '',
    bottomLeftText: '',
    bottomRightText: '',
    border: '',
  },
)

// Validation: Ensure only 2 or fewer text overlays are active
const activeTextCount = computed(() => {
  let count = 0
  if (props.topLeftText) count++
  if (props.topRightText) count++
  if (props.bottomLeftText) count++
  if (props.bottomRightText) count++
  return count
})

// Warn if more than 2 text overlays are provided
if (activeTextCount.value > 2) {
  console.warn(
    'VideoOverlay: More than 2 text overlays provided. Consider using only 2 for better readability.',
  )
}
</script>
