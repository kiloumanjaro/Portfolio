<template>
  <button
    ref="button1"
    @mouseenter="handleButtonEnter($event)"
    @mouseleave="handleButtonLeave"
    @mousemove="handleButtonMove"
    class="overflow-hidden bg-[#232323] w-full group transition-transform duration-100 ease-out"
    :class="rounded"
    :style="{ transform: buttonScale }"
  >
    <!-- Ripple effect element -->
    <div
      class="absolute pointer-events-none rounded-full bg-[#393939]"
      :style="{
        left: rippleStyle.left,
        top: rippleStyle.top,
        transform: rippleStyle.transform,
        opacity: rippleStyle.opacity,
        width: '60px',
        height: '60px',
        marginLeft: '-30px',
        marginTop: '-30px',
        transition: 'all 250ms cubic-bezier(0.4, 0, 0.2, 1)',
      }"
    ></div>

    <span
      class="relative top-[1px] flex items-center justify-center transition-transform duration-200 ease-out"
      :style="{ transform: buttonTransform }"
    >
      <div v-if="icon">
        <v-icon :icon="icon" size="30" />
      </div>
    </span>
  </button>
</template>

<script setup lang="ts">
import { ref, inject, type Ref } from 'vue'

defineProps<{
  icon?: string
  name?: string
  rounded?: string
}>()

const buttonTransform = ref('translate(0, 0)')
const buttonScale = ref('scale(1)')
const currentButton = ref<HTMLElement | null>(null)
const rippleStyle = ref({
  left: '0px',
  top: '0px',
  transform: 'scale(0.1)',
  opacity: '0',
})

const cursorState = inject('cursorState') as {
  cursorColor: Ref<string>
  cursorScale: Ref<string>
  cursorClass: Ref<string>
}

const handleButtonEnter = (e: MouseEvent) => {
  const button = e.currentTarget as HTMLElement
  currentButton.value = button
  cursorState.cursorColor.value = 'transparent'
  cursorState.cursorClass.value = ''

  // Button scale animation - quick enlarge then back to normal
  buttonScale.value = 'scale(1.02)'
  setTimeout(() => {
    buttonScale.value = 'scale(1)'
  }, 80)

  // Calculate cursor position relative to button
  const rect = button.getBoundingClientRect()
  const x = e.clientX - rect.left
  const y = e.clientY - rect.top

  // Calculate the maximum distance to cover the entire button
  const maxDistance = Math.sqrt(
    Math.pow(Math.max(x, rect.width - x), 2) + Math.pow(Math.max(y, rect.height - y), 2),
  )

  // Start with small scale and visible
  rippleStyle.value = {
    left: `${x}px`,
    top: `${y}px`,
    transform: 'scale(0.1)', // Start small but visible
    opacity: '0.8',
  }

  // Animate to full size
  requestAnimationFrame(() => {
    requestAnimationFrame(() => {
      rippleStyle.value = {
        left: `${x}px`,
        top: `${y}px`,
        transform: `scale(${maxDistance / 30})`, // Larger final scale for better coverage
        opacity: '1',
      }
    })
  })
}

const handleButtonLeave = () => {
  currentButton.value = null
  cursorState.cursorColor.value = '#393939'
  cursorState.cursorClass.value = ''
  buttonTransform.value = 'translate(0, 0)'
  buttonScale.value = 'scale(1)' // Reset scale on leave

  // Reset to small scale
  rippleStyle.value = {
    left: '0px',
    top: '0px',
    transform: 'scale(0.1)',
    opacity: '0',
  }
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
