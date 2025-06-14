<script setup lang="ts">
import ButtonComponent from './ButtonComponent.vue'
import IntroductionText from './IntroductionText.vue'
</script>

<template>
  <div class="flex justify-center">
    <div class="flex flex-col justify-center bg-blue-600 w-4xl h-80 gap-5">
      <IntroductionText
        title="Kint Louise is a creative developer at"
        description="My passion is create emotional experiences
at the intersection of art, design, and AI."
      />
      <ButtonComponent text="Skillset" />
    </div>
  </div>
</template>
