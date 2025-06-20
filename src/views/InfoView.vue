<script setup lang="ts">
import ContactSection from '@/components/layouts/ContactSection.vue'
import InformationSection from '@/components/layouts/InformationSection.vue'
import AccoladesSection from '@/components/layouts/AccoladesSection.vue'
import TechstackSection from '@/components/layouts/TechstackSection.vue'
import ProfilePictureComponent from '@/components/ProfilePictureComponent.vue'
import TimelineClockComponent from '@/components/TimelineClockComponent.vue'
</script>

<template>
  <main>
    <TimelineClockComponent />
  </main>
  <div class="py-30">
    <div class="flex flex-col items-center gap-28">
      <div class="flex flex-col items-center gap-10">
        <ProfilePictureComponent />
        <InformationSection />
        <TechstackSection />
      </div>
      <ContactSection />
      <AccoladesSection />
    </div>
  </div>
</template>

<style></style>
