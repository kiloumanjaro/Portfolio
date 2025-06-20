<script setup lang="ts">
import AnimatedButtonComponent from '../AnimatedButtonComponent.vue'
import AvailabilityComponent from '../AvailabilityComponent.vue'
import IntroductionText from '../IntroductionText.vue'
import TrustedByComponent from '../TrustedByComponent.vue'
</script>

<template>
  <div class="flex flex-col items-center gap-10">
    <div class="flex flex-col items-center gap-8">
      <AvailabilityComponent size="sm" status-text="Available for new project" />
      <IntroductionText
        title="Kint Louise is an aspiring web designer"
        description="My passion is create emotional experiences
at the intersection of art, design, and AI. My passion is create emotional  "
      />
    </div>

    <div class="flex flex-row gap-5">
      <!-- <div class="w-30">
        <AnimatedButtonComponent name="Click" rounded="rounded-3xl" />
      </div> -->
      <TrustedByComponent />
    </div>
  </div>
</template>
