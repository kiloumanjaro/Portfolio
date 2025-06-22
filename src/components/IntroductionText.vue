<script setup lang="ts">
defineProps<{
  title: string
  description: string
  role: string
}>()
</script>

<template>
  <div class="flex flex-col items-center">
    <div class="relative gap-7 w-7/12">
      <div class="flex items-center justify-center gap-2">
        <h1 class="text-5xl font-medium">{{ title }}</h1>
        <div class="w-5 h-5 bg-red-500"></div>
      </div>
      <!-- <h1
        class="absolute flex text-amber-300 flex-col items-start text-5xl bottom-0 right-[64px] font-medium bg-[#181818]"
      >
        {{ role }}
      </h1> -->
    </div>
    <h3 class="w-3/4">{{ description }}</h3>
  </div>
</template>

<style scoped></style>
