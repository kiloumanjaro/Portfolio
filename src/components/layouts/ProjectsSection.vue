<script setup lang="ts">
import WhiteVideoPlaceHolderComponent from '../WVideoPlaceHolderComponent.vue'
import BlackVideoPlaceHolderComponent from '../BVideoPlaceHolderComponent.vue'
import AnimatedButtonComponent from '../VideoButtonComponent.vue'
import sidebar from '@/assets/videos/sidebar.mp4'
import word from '@/assets/videos/word-lookup.mp4'
import dock from '@/assets/videos/dock-drag.mp4'
import slider from '@/assets/videos/fractional-slider.mp4'
import vanish from '@/assets/videos/vanish-input.mp4'
import peach from '@/assets/videos/peach.mp4'
import checkbox from '@/assets/videos/checkbox.mp4'
import footer from '@/assets/videos/vercel-footer-2.mp4'
const border = 'border border-[#2e2e2e]'
</script>

<template>
  <div class="grid grid-cols-3 grid-rows-4 gap-2 w-5xl">
    <div class="col-span-2 flex flex-col bg-[#1c1c1c] border border-[#2e2e2e] p-1 rounded-xl gap-1">
      <WhiteVideoPlaceHolderComponent
        :videoSrc="sidebar"
        topLeftText="Sidebar"
        topRightText="February 2025"
      />
      <AnimatedButtonComponent name="Click" rounded="rounded-lg" />
    </div>

    <BlackVideoPlaceHolderComponent
      :videoSrc="word"
      topLeftText="Word Lookup"
      topRightText="January 2024"
      :border="border"
    />

    <WhiteVideoPlaceHolderComponent
      :videoSrc="dock"
      bottomLeftText="SwiftUI Dock"
      bottomRightText="December 2023"
      :border="border"
    />

    <WhiteVideoPlaceHolderComponent
      :videoSrc="slider"
      bottomLeftText="Fractional Slider"
      bottomRightText="January 2023"
      :border="border"
      class="col-span-2"
    />

    <WhiteVideoPlaceHolderComponent
      :videoSrc="vanish"
      bottomLeftText="Vanish Input"
      bottomRightText="January 2023"
      :border="border"
    />

    <WhiteVideoPlaceHolderComponent
      :videoSrc="peach"
      bottomLeftText="Tangerine Shader"
      bottomRightText="September 2022"
      :border="border"
    />

    <WhiteVideoPlaceHolderComponent
      :videoSrc="checkbox"
      bottomLeftText="Animated Checkboxes"
      bottomRightText="November 2021"
      :border="border"
      class="row-span-2"
    />

    <WhiteVideoPlaceHolderComponent
      :videoSrc="footer"
      bottomLeftText="Animated Checkboxes"
      bottomRightText="November 2021"
      :border="border"
      class="col-span-2"
    />
  </div>
</template>
