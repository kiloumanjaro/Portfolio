<script setup lang="ts">
defineProps<{
  href: string
  title: string
}>()
</script>

<template>
  <a
    :href="href"
    target="_blank"
    rel="noopener"
    class="flex flex-row items-center gap-1 hover:text-blue-500"
  >
    {{ title }}

    <v-icon icon="mdi-arrow-top-right" size="20" class="relative -mt-[2px]" />
  </a>
</template>
