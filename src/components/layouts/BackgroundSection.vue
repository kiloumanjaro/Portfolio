<template>
  <div class="flex flex-col justify-center w-4xl gap-9">
    <div class="flex flex-col gap-3">
      <h1 class="text-2xl">Background</h1>
      <p>
        Designing is an essential part of my process. My essays were featured on FastCompany, TNW,
        Smashing Magazine, and Medium. You can find some of my latest writing below.
      </p>
    </div>
    <div class="grid grid-cols-3 gap-4">
      <div class="flex flex-col gap-3">
        <AnimatedButtonComponent class="h-48" icon="mdi-youtube" rounded="rounded-md" />
        <p>How Apple beat Swiss watchmakers at their own game</p>
      </div>
      <div class="flex flex-col gap-3">
        <AnimatedButtonComponent class="h-48" icon="mdi-alpha-b-box-outline" rounded="rounded-md" />
        <p>My chatbot is dead</p>
      </div>
      <div class="flex flex-col gap-3">
        <AnimatedButtonComponent class="h-48" icon="mdi-facebook" rounded="rounded-md" />
        <p>The rise of Anti-notifications</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import AnimatedButtonComponent from '../AnimatedButtonComponent.vue'
</script>
