<script setup lang="ts">
import IntroductionSection from '@/components/layouts/IntroductionSection.vue'
import ProjectsSection from '@/components/layouts/ProjectsSection.vue'
import DesignBackgroundSection from '@/components/layouts/DesignBackgroundSection.vue'
import CodingBackgroundSection from '@/components/layouts/CodingBackgroundSection.vue'
import TimelineClockComponent from '@/components/TimelineClockComponent.vue'
import FooterSection from '@/components/layouts/FooterSection.vue'
import ExpandbaleComponent from '@/components/ExpandbaleComponent.vue'
</script>

<template>
  <main>
    <TimelineClockComponent />
    <div class="flex flex-col items-center pt-25 pb-20 gap-15">
      <IntroductionSection />
      <view class="flex h-[900px]">
        <ProjectsSection />
      </view>
      <span>
        <CodingBackgroundSection />
        <ExpandbaleComponent />
      </span>

      <DesignBackgroundSection />
    </div>
  </main>
  <footer>
    <FooterSection />
  </footer>
</template>
