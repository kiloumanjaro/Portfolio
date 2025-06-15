<script setup lang="ts">
defineProps<{
  text: string
}>()
</script>

<template>
  <button
    class="flex w-30 justify-center gap-2 px-5 py-3 bg-[#232323] text-white rounded-3xl cursor-pointer transition-colors duration-200 ease-in-out hover:bg-[#333333]"
  >
    <h3 class="text-l">
      {{ text }}
    </h3>
  </button>
</template>

<style scoped></style>
