<template>
  <div class="flex items-center gap-3">
    <div class="flex flex-row">
      <div
        v-for="(avatar, index) in avatars"
        :key="index"
        class="w-8 h-10"
        :style="{ left: `${index * 24}px`, zIndex: index }"
      >
        <div class="shrink-0 w-10 h-10 relative right-2">
          <img
            :src="avatar"
            :alt="`Founder ${index + 1}`"
            class="w-10 h-10 rounded-full border-3 border-[#181818]"
          />
        </div>
      </div>
    </div>

    <span class="text-sm font-normal">
      {{ trustText }}
    </span>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Static data
const avatars = ref<string[]>([
  'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=100&h=100&fit=crop&crop=face',
  'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=100&h=100&fit=crop&crop=face',
  'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=100&h=100&fit=crop&crop=face',
  'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?w=100&h=100&fit=crop&crop=face',
])

const trustText = ref('Trusted by 25+ founders')
</script>
