<template>
  <div class="inline-flex items-center gap-3 px-5 py-4 rounded-lg border border-gray-700 min-w-3xs">
    <div class="shrink-0">
      <v-icon :icon="icon" size="35" />
    </div>
    <div class="flex flex-col justify-between w-full h-8">
      <h2 class="text-white font-medium text-sm">{{ title }}</h2>
      <div class="w-full bg-gray-700 rounded-full h-1">
        <div class="bg-yellow-400 h-1 rounded-full" :style="{ width: width }"></div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  icon: string
  title: string
  width: string
}>()
</script>
