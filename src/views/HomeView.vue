<script setup lang="ts">
import IntroductionSection from '@/components/layouts/IntroductionSection.vue'
import ProjectsSection from '@/components/layouts/ProjectsSection.vue'
import BackgroundSection from '@/components/layouts/BackgroundSection.vue'
</script>

<template>
  <main class="py-10">
    <div class="flex flex-col items-center gap-10">
      <IntroductionSection />
      <ProjectsSection />
      <BackgroundSection />
    </div>
  </main>
</template>
