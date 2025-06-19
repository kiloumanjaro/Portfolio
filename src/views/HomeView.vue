<script setup lang="ts">
import IntroductionSection from '@/components/layouts/IntroductionSection.vue'
import ProjectsSection from '@/components/layouts/ProjectsSection.vue'
import DesignBackgroundSection from '@/components/layouts/DesignBackgroundSection.vue'
import CodingBackgroundSection from '@/components/layouts/CodingBackgroundSection.vue'
import TimelineClockComponent from '@/components/TimelineClockComponent.vue'
</script>

<template>
  <main>
    <TimelineClockComponent />
    <div class="flex flex-col items-center pt-40 gap-15">
      <IntroductionSection />
      <view class="flex h-[900px]">
        <ProjectsSection />
      </view>
      <DesignBackgroundSection />
      <CodingBackgroundSection />
    </div>
  </main>
</template>
