<script setup lang="ts">
import ContactSection from '@/components/layouts/ContactSection.vue'
import InformationSection from '@/components/layouts/InformationSection.vue'
import ProjectionSection from '@/components/layouts/ProjectionSection.vue'
import ProfilePictureComponent from '@/components/ProfilePictureComponent.vue'
</script>

<template>
  <div class="py-10">
    <div class="flex flex-col items-center gap-10">
      <ProfilePictureComponent />
      <InformationSection />
      <ContactSection />
      <ProjectionSection />
    </div>
  </div>
</template>

<style></style>
