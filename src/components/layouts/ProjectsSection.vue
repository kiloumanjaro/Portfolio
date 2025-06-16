<script setup lang="ts">
import VideoPlaceHolderComponent from '../WVideoPlaceHolderComponent.vue'
import sidebar from '@/assets/videos/sidebar.mp4'
</script>

<template>
  <div class="grid grid-cols-5 grid-rows-2 gap-2 w-11/12 h-96">
    <VideoPlaceHolderComponent
      :videoSrc="sidebar"
      topLeftText="Sidebar"
      topRightText="February 2025"
      class="col-span-2"
    />
    <div class="bg-red-300 p-4 rounded-lg">1</div>
    <div class="bg-green-300 p-4 rounded-lg">2</div>
    <div class="bg-blue-300 p-4 row-span-2 rounded-lg">3</div>
    <div class="bg-yellow-300 p-4 rounded-lg">4</div>
    <div class="bg-pink-300 p-4 rounded-lg">5</div>
    <div class="bg-purple-300 p-4 col-span-2 rounded-lg">6</div>
  </div>
</template>
