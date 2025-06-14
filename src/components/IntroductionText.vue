<script setup lang="ts">
defineProps<{
  title: string
  description: string
}>()
</script>

<template>
  <div class="flex flex-col gap-3">
    <h1 class="text-3xl w-1/2">{{ title }}</h1>
    <h3 class="w-2/5">{{ description }}</h3>
    <i>
      <slot name="icon"></slot>
    </i>
  </div>
</template>

<style scoped></style>
