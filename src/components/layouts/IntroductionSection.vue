<script setup lang="ts">
import AnimatedButtonComponent from '../AnimatedButtonComponent.vue'
import IntroductionText from '../IntroductionText.vue'
import TimelineClockComponent from '../TimelineClockComponent.vue'
</script>

<template>
  <div class="flex flex-col justify-center gap-10">
    <IntroductionText
      title="Kint Louise is an aspiring web designer"
      description="My passion is create emotional experiences
at the intersection of art, design, and AI."
    />
    <div class="w-30">
      <AnimatedButtonComponent name="Click" rounded="rounded-3xl" />
    </div>
    <TimelineClockComponent />
  </div>
</template>
