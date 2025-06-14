<script setup lang="ts">
defineProps<{
  text: string
}>()
</script>

<template>
  <button
    class="flex w-32 justify-center gap-2 px-5 py-3 bg-indigo-400 rounded-3xl cursor-pointer transition-colors duration-200 ease-in-out hover:bg-indigo-700"
  >
    <h3 class="text-l">
      {{ text }}
    </h3>
  </button>
</template>

<style scoped></style>
