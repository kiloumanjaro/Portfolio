<script setup lang="ts">
import { RouterView } from 'vue-router'
import AnimatedLinkComponent from './components/AnimatedLinkComponent.vue'
import TabsComponent from './components/TabsComponent.vue'
import { ref, onMounted, onUnmounted, provide } from 'vue'

const cursor = ref<HTMLElement | null>(null)
const cursorX = ref(0)
const cursorY = ref(0)
const cursorColor = ref('#393939')
const cursorScale = ref(1)
const cursorClass = ref('')

const updateCursorPosition = (e: MouseEvent) => {
  cursorX.value = e.clientX
  cursorY.value = e.clientY
}

provide('cursorState', {
  cursorColor,
  cursorScale,
  cursorClass,
})

onMounted(() => {
  document.addEventListener('mousemove', updateCursorPosition)
  document.body.style.cursor = 'none'
})
onUnmounted(() => {
  document.removeEventListener('mousemove', updateCursorPosition)
  document.body.style.cursor = 'auto'
})
</script>

<template>
  <div class="cursor-none">
    <div
      ref="cursor"
      class="fixed rounded-full pointer-events-none z-[9999]"
      :class="cursorClass"
      :style="{
        left: cursorX + 'px',
        top: cursorY + 'px',
        width: 36 * cursorScale + 'px',
        height: 36 * cursorScale + 'px',
        transform: 'translate(-50%, -50%)',
        backgroundColor: cursorColor,
      }"
    ></div>

    <header>
      <div class="flex flex-row w-full p-10 justify-between items-center">
        <TabsComponent />
        <div class="flex gap-3 text-white">
          <a
            href="https://www.linkedin.com/in/kint-louise-borbano-6982a4327/"
            target="_blank"
            rel="noopener"
          >
            <AnimatedLinkComponent name="LinkedIn" rounded="rounded-md" />
          </a>
          <a href="https://github.com/kiloumanjaro" target="_blank" rel="noopener">
            <AnimatedLinkComponent name="GitHub" rounded="rounded-md" />
          </a>
        </div>
      </div>
    </header>

    <div>
      <RouterView />
    </div>
  </div>
</template>

<style scoped>
.cursor-none * {
  cursor: none !important;
}
</style>
