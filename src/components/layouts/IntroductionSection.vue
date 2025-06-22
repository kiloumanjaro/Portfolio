<script setup lang="ts">
import AnimatedButtonComponent from '../AnimatedButtonComponent.vue'
import AvailabilityComponent from '../AvailabilityComponent.vue'
import IntroductionText from '../IntroductionText.vue'
import TrustedByComponent from '../TrustedByComponent.vue'
const role = 'web design'
</script>

<template>
  <div class="flex flex-col items-center gap-10">
    <div class="flex flex-col items-center gap-8">
      <AvailabilityComponent size="sm" status-text="Available for new project" />
      <IntroductionText
        title="a creative force in"
        :role="role"
        description="With a strong background in design and a passion for technology, I merge creativity and code to craft expressive interfaces that don’t just function — they feel."
      />
    </div>

    <div class="flex flex-row gap-5">
      <!-- <div class="w-30">
        <AnimatedButtonComponent name="Click" rounded="rounded-3xl" />
      </div> -->
    </div>
  </div>
</template>
