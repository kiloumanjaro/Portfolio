<script setup lang="ts">
import { ref, onMounted } from 'vue'

defineProps<{
  title: string
  description: string
  role: string
}>()

const roles = ['web development', 'graphic design', 'software engineering']
const currentRoleIndex = ref(0)
const isAnimating = ref(false)

const nextRole = () => {
  if (isAnimating.value) return

  isAnimating.value = true
  currentRoleIndex.value = (currentRoleIndex.value + 1) % roles.length

  setTimeout(() => {
    isAnimating.value = false
  }, 300)
}

onMounted(() => {
  setInterval(() => {
    nextRole()
  }, 3000)
})
</script>

<template>
  <div class="flex flex-col items-center gap-7 w-4xl">
    <div class="flex flex-col items-center w-xl">
      <h1 class="text-5xl font-medium">{{ title }}</h1>
      <div
        @click="nextRole"
        class="text-5xl font-medium select-none relative group"
        :class="{ 'animate-pulse': isAnimating }"
      >
        <span
          class="relative z-10 transition-all duration-300 ease-in-out group-hover:text-blue-600 group-hover:scale-105 leading-tight"
          :class="{ 'transform scale-95 opacity-70': isAnimating }"
        >
          {{ roles[currentRoleIndex] }}
        </span>
      </div>
    </div>
    <h3 class="w-8/12 text-center">{{ description }}</h3>
  </div>
</template>
