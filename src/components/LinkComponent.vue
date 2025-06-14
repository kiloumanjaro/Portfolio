<script setup lang="ts">
import NorthEast from './icons/NorthEast.vue'
defineProps<{
  href: string
  title: string
}>()
</script>

<template>
  <a :href="href" target="_blank" rel="noopener" class="flex flex-row">
    {{ title }}
    <NorthEast />
  </a>
</template>
