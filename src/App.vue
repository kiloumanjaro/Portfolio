<script setup lang="ts">
import { RouterView } from 'vue-router'
import LinkComponent from './components/LinkComponent.vue'
import TabsComponent from './components/TabsComponent.vue'
import { ref, onMounted, onUnmounted } from 'vue'
const cursor = ref(null)
const cursorX = ref(0)
const cursorY = ref(0)
const updateCursorPosition = (e: MouseEvent) => {
  cursorX.value = e.clientX
  cursorY.value = e.clientY
}

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
      class="fixed w-9 h-9 bg-[#393939] hover:bg-black rounded-full pointer-events-none z-[9999] transition-transform duration-100 ease-out"
      :style="{
        left: cursorX + 'px',
        top: cursorY + 'px',
        transform: 'translate(-50%, -50%)',
      }"
    ></div>

    <header>
      <div class="flex flex-row w-full p-10 justify-between items-center">
        <h1 class="text-lg font-bold text-white">KILOU</h1>
        <div class="flex gap-12 text-white">
          <LinkComponent
            title="LinkedIn"
            href="https://www.linkedin.com/in/kint-louise-borbano-6982a4327/"
          />
          <LinkComponent title="GitHub" href="https://github.com/kiloumanjaro" />
        </div>
        <div class="absolute left-1/2 transform -translate-x-1/2">
          <TabsComponent />
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
