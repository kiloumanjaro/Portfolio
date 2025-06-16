<template>
  <button
    ref="button1"
    @mouseenter="handleButtonEnter($event, '#3b82f6')"
    @mouseleave="handleButtonLeave"
    @mousemove="handleButtonMove"
    class="relative overflow-hidden bg-[#232323] hover:bg-[#393939] text-white px-6 py-3 rounded-md transition-colors w-full group"
  >
    <span
      class="relative z-10 flex items-center justify-center transition-transform duration-200 ease-out"
      :style="{ transform: buttonTransform }"
    >
      <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M13 10V3L4 14h7v7l9-11h-7z"
        ></path>
      </svg>
      Primary Action
    </span>
  </button>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const cursorColor = ref('#000000')
const cursorScale = ref(1)
const cursorClass = ref('bg-black')

const buttonTransform = ref('translate(0, 0)')
const currentButton = ref<HTMLElement | null>(null)

const handleButtonEnter = (e: MouseEvent, color: string) => {
  const button = e.currentTarget as HTMLElement
  currentButton.value = button
  cursorColor.value = color
  cursorScale.value = 1.5
  cursorClass.value = ''
}

const handleButtonLeave = () => {
  currentButton.value = null
  cursorColor.value = '#000000'
  cursorScale.value = 1
  cursorClass.value = 'bg-black'
  buttonTransform.value = 'translate(0, 0)'
}

const handleButtonMove = (e: MouseEvent) => {
  if (!currentButton.value) return

  const button = currentButton.value
  const rect = button.getBoundingClientRect()
  const buttonCenterX = rect.left + rect.width / 2
  const buttonCenterY = rect.top + rect.height / 2
  const deltaX = e.clientX - buttonCenterX
  const deltaY = e.clientY - buttonCenterY
  const maxMove = 8
  const moveX = Math.max(-maxMove, Math.min(maxMove, deltaX * 0.3))
  const moveY = Math.max(-maxMove, Math.min(maxMove, deltaY * 0.3))

  buttonTransform.value = `translate(${moveX}px, ${moveY}px)`
}
</script>
