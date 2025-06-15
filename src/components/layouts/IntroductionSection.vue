<script setup lang="ts">
import ButtonComponent from '../ButtonComponent.vue'
import IntroductionText from '../IntroductionText.vue'
</script>

<template>
  <div class="flex flex-col justify-center w-4xl h-80 gap-10">
    <IntroductionText
      title="Kint Louise is a web designer from the Philippines"
      description="My passion is create emotional experiences
at the intersection of art, design, and AI."
    />
    <ButtonComponent text="Skillset" />
  </div>
</template>
