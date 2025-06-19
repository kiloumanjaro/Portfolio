<script setup lang="ts">
import IntroductionSection from '@/components/layouts/IntroductionSection.vue'
import ProjectsSection from '@/components/layouts/ProjectsSection.vue'
import BackgroundSection from '@/components/layouts/BackgroundSection.vue'
import TimelineClockComponent from '@/components/TimelineClockComponent.vue'
</script>

<template>
  <main>
    <TimelineClockComponent />
    <div class="flex flex-col items-center gap-15">
      <IntroductionSection />
      <view class="flex h-[900px]">
        <ProjectsSection />
      </view>
      <BackgroundSection />
    </div>
  </main>
</template>
