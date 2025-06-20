<script setup lang="ts">
defineProps<{
  title: string
  description: string
}>()
</script>

<template>
  <div class="flex flex-col gap-7 items-center">
    <h1 class="text-5xl text-center font-medium w-7/12">{{ title }}</h1>
    <h3 class="w-3/4">{{ description }}</h3>
  </div>
</template>

<style scoped></style>
