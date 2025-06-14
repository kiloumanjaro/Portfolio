<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue'

const props = defineProps({
  text: {
    type: String,
    default: '',
  },
  tag: {
    type: String,
    default: 'p',
  },
  duration: {
    type: Number,
    default: 2000,
  },
  delay: {
    type: Number,
    default: 0,
  },
  speed: {
    type: Number,
    default: 50,
  },
  className: {
    type: String,
    default: '',
  },
  autoStart: {
    type: Boolean,
    default: true,
  },
})

const scrambledText = ref<string>('')
const interval = ref<ReturnType<typeof setInterval> | null>(null)
const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+-=[]{}|;:,.<>?'
const getRandomChar = (): string => {
  return characters[Math.floor(Math.random() * characters.length)]
}

const scrambleText = (targetText: string, revealedCount: number): string => {
  let result = ''

  for (let i = 0; i < targetText.length; i++) {
    if (i < revealedCount) {
      result += targetText[i]
    } else if (targetText[i] === ' ') {
      result += ' '
    } else {
      result += getRandomChar()
    }
  }

  return result
}

const startAnimation = (): void => {
  if (!props.text) return

  // Initialize with scrambled text
  scrambledText.value = props.text.replace(/[^\s]/g, () => getRandomChar())

  const startTime = Date.now()
  let revealedCount = 0

  interval.value = setInterval(() => {
    const elapsed = Date.now() - startTime
    const progress = Math.min(elapsed / props.duration, 1)

    const targetRevealed = Math.floor(progress * props.text.length)

    if (targetRevealed > revealedCount) {
      revealedCount = targetRevealed
    }

    scrambledText.value = scrambleText(props.text, revealedCount)

    if (progress >= 1 && revealedCount >= props.text.length) {
      if (interval.value) {
        clearInterval(interval.value)
        interval.value = null
      }
      scrambledText.value = props.text
    }
  }, props.speed)
}

const stopAnimation = (): void => {
  if (interval.value !== null) {
    clearInterval(interval.value)
    interval.value = null
  }
}

const resetAnimation = (): void => {
  stopAnimation()
  scrambledText.value = props.text.replace(/[^\s]/g, () => getRandomChar())
}

defineExpose({
  start: startAnimation,
  stop: stopAnimation,
  reset: resetAnimation,
})

watch(
  () => props.text,
  () => {
    if (props.autoStart) {
      stopAnimation()
      setTimeout(startAnimation, props.delay)
    }
  },
  { immediate: false },
)

onMounted(() => {
  if (props.autoStart && props.text) {
    setTimeout(startAnimation, props.delay)
  }
})

onUnmounted(() => {
  stopAnimation()
})
</script>

<template>
  <component
    :is="tag"
    :class="['font-mono tracking-wide transition-colors duration-200', className]"
    v-bind="$attrs"
  >
    {{ scrambledText || text }}
  </component>
</template>
