<script setup lang="ts">
import AnimatedButtonComponent from '../AnimatedButtonComponent.vue'
import IntroductionText from '../IntroductionText.vue'
</script>

<template>
  <div class="flex flex-col justify-center w-4xl h-80 gap-10">
    <IntroductionText
      title="Kint Louise is a web designer from the Philippines"
      description="My passion is create emotional experiences
at the intersection of art, design, and AI."
    />
    <div class="w-30">
      <AnimatedButtonComponent name="Click" rounded="rounded-3xl" />
    </div>
  </div>
</template>
