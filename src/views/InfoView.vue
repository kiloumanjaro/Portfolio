<script setup lang="ts">
import ContactSection from '@/components/layouts/ContactSection.vue'
import InformationSection from '@/components/layouts/InformationSection.vue'
import ProfilePictureComponent from '@/components/ProfilePictureComponent.vue'
</script>

<template>
  <div class="py-10">
    <div class="flex flex-col items-center gap-10">
      <ProfilePictureComponent />
      <InformationSection />
      <ContactSection />
    </div>
  </div>
</template>

<style></style>
