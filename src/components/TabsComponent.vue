<template>
  <div class="flex items-center justify-center">
    <div
      ref="tabsContainer"
      @mouseenter="handleTabsEnter($event)"
      @mouseleave="handleTabsLeave"
      class="relative bg-[#232323] rounded-full p-1 flex transition-transform duration-100 ease-out overflow-hidden"
      :style="{ transform: tabsScale }"
    >
      <!-- Ripple effect element -->
      <div
        class="absolute pointer-events-none rounded-full bg-[#393939] z-0"
        :style="{
          left: rippleStyle.left,
          top: rippleStyle.top,
          transform: rippleStyle.transform,
          opacity: rippleStyle.opacity,
          width: '60px',
          height: '60px',
          marginLeft: '-30px',
          marginTop: '-30px',
          transition: 'all 50ms cubic-bezier(0.4, 0, 0.2, 1)',
        }"
      ></div>

      <!-- Tab content with movement -->
      <div
        class="relative z-10 flex transition-transform duration-200 ease-out"
        :style="{ transform: tabsTransform }"
      >
        <RouterLink to="/">
          <button
            @click="activeTab = 'work'"
            @mouseenter="hoveredButton = 'work'"
            @mouseleave="hoveredButton = null"
            :class="[
              'px-6 py-2 rounded-full text-sm transition-all duration-200',
              getButtonClass('work'),
            ]"
          >
            Work
          </button>
        </RouterLink>

        <RouterLink to="/info">
          <button
            @click="activeTab = 'info'"
            @mouseenter="hoveredButton = 'info'"
            @mouseleave="hoveredButton = null"
            :class="[
              'px-6 py-2 rounded-full text-sm transition-all duration-200',
              getButtonClass('info'),
            ]"
          >
            Info
          </button>
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { ref, inject, type Ref } from 'vue'

const activeTab = ref('work')
const hoveredButton = ref<string | null>(null)
const isContainerHovered = ref(false)
const tabsContainer = ref<HTMLElement | null>(null)
const tabsTransform = ref('translate(0, 0)')
const tabsScale = ref('scale(1)')

const cursorState = inject('cursorState') as {
  cursorColor: Ref<string>
  cursorScale: Ref<string>
  cursorClass: Ref<string>
}

const rippleStyle = ref({
  left: '0px',
  top: '0px',
  transform: 'scale(0.1)',
  opacity: '0',
})

// Computed function to determine button styling
const getButtonClass = (buttonName: string) => {
  // If hovering over this specific button
  if (hoveredButton.value === buttonName) {
    return 'bg-[#232323] text-white'
  }

  // If container is hovered but not this specific button
  if (isContainerHovered.value && hoveredButton.value !== buttonName) {
    return 'bg-[#393939] text-gray-400'
  }

  // Default state (not hovering container)
  if (activeTab.value === buttonName) {
    return 'bg-[#393939] text-white'
  } else {
    return 'text-gray-400 hover:text-gray-400'
  }
}

function handleTabsEnter(event: MouseEvent) {
  const container = event.currentTarget as HTMLElement
  tabsContainer.value = container
  isContainerHovered.value = true
  cursorState.cursorColor.value = 'transparent'

  // Tabs scale animation - quick enlarge then back to normal
  tabsScale.value = 'scale(1.05)'

  // Calculate cursor position relative to container
  const rect = container.getBoundingClientRect()
  const x = event.clientX - rect.left
  const y = event.clientY - rect.top

  // Calculate the maximum distance to cover the entire container
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

function handleTabsLeave() {
  tabsContainer.value = null
  isContainerHovered.value = false
  hoveredButton.value = null
  cursorState.cursorColor.value = '#393939'
  tabsTransform.value = 'translate(0, 0)'
  tabsScale.value = 'scale(1)'

  // Properly fade out the ripple
  rippleStyle.value = {
    left: rippleStyle.value.left, // Keep current position
    top: rippleStyle.value.top, // Keep current position
    transform: rippleStyle.value.transform, // Keep current scale
    opacity: '0', // Fade out
  }

  // After transition completes, reset everything
  setTimeout(() => {
    rippleStyle.value = {
      left: '0px',
      top: '0px',
      transform: 'scale(0.1)',
      opacity: '0',
    }
  }, 250) // Match the transition duration
}
</script>
