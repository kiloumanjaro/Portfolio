<script setup lang="ts">
defineProps<{
  title: string
  description: string
}>()
</script>

<template>
  <div class="flex flex-col gap-7">
    <h1 class="text-4xl font-medium w-7/12">{{ title }}</h1>
    <h3 class="w-2/5">{{ description }}</h3>
  </div>
</template>

<style scoped></style>
