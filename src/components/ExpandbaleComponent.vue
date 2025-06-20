<template>
  <div class="flex items-center justify-center p-8">
    <div class="flex flex-col items-center">
      <div
        class="transition-all duration-500 ease-in-out overflow-hidden"
        :class="{
          'w-4xl h-0': !isExpanded,
          'w-4xl h-auto': isExpanded,
        }"
      >
        <div
          class="flex flex-col transition-all duration-500 ease-in-out gap-10"
          :class="{
            'opacity-0 scale-95': !isExpanded,
            'opacity-100 scale-100': isExpanded,
          }"
        >
          <span class="flex flex-row justify-between">
            <div class="flex flex-col gap-1">
              <p class="font-bold mb-4">The Power of Unfinished (10 min)</p>
              <p class="mb-4 font-light">How to get more done, uplevel your craft</p>
            </div>
            <div class="flex flex-row gap-3">
              <div class="w-13 h-13">
                <AnimatedSquareButtonComponent icon="mdi-open-in-new" rounded="rounded-md" />
              </div>
              <div class="w-13 h-13">
                <AnimatedSquareButtonComponent icon="mdi-github" rounded="rounded-md" />
              </div>
            </div>
          </span>

          <span class="flex flex-row justify-between">
            <div class="flex flex-col gap-1">
              <p class="font-bold mb-4">The Power of Unfinished (10 min)</p>
              <p class="mb-4 font-light">How to get more done, uplevel your craft</p>
            </div>
            <div class="flex flex-row gap-3">
              <div class="w-13 h-13">
                <AnimatedSquareButtonComponent icon="mdi-open-in-new" rounded="rounded-md" />
              </div>
              <div class="w-13 h-13">
                <AnimatedSquareButtonComponent icon="mdi-github" rounded="rounded-md" />
              </div>
            </div>
          </span>
        </div>
      </div>
      <div class="w-16">
        <AnimatedCircleButtonComponent
          @click="toggleExpanded"
          class="rounded-full h-16 transition-all duration-500 ease-in-out z-10"
          :class="{
            'transform translate-y-0': !isExpanded,
            'transform translate-y-4': isExpanded,
          }"
          :icon="isExpanded ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        >
        </AnimatedCircleButtonComponent>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import AnimatedCircleButtonComponent from './AnimatedCircleButtonComponent.vue'
import AnimatedSquareButtonComponent from './AnimatedSquareButtonComponent.vue'

const isExpanded = ref(false)

const toggleExpanded = () => {
  isExpanded.value = !isExpanded.value
}
</script>
