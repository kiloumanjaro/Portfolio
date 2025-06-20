<template>
  <div class="border-t border-gray-400/20 my-4"></div>
  <div class="flex flex-col w-full py-15 px-30 gap-10">
    <div class="flex flex-row justify-between">
      <div>Logo</div>
      <div class="flex flex-row gap-10">
        <div class="flex flex-col gap-3">
          <h2 class="text-sm px-5">Main</h2>
          <div class="flex flex-col w-32 gap-2">
            <AnimatedLinkComponent name="Work" rounded="rounded-md" justify="left" />

            <RouterLink to="/info">
              <AnimatedLinkComponent name="Info" rounded="rounded-md" justify="left" />
            </RouterLink>
          </div>
        </div>
        <div class="flex flex-col gap-3">
          <h2 class="text-sm px-5">Contact</h2>
          <div class="flex flex-col w-32 gap-2">
            <a
              href="https://www.linkedin.com/in/kint-louise-borbano-6982a4327/"
              target="_blank"
              rel="noopener"
            >
              <AnimatedLinkComponent name="LinkedIn" rounded="rounded-md" justify="left" />
            </a>
            <a href="https://github.com/kiloumanjaro" target="_blank" rel="noopener">
              <AnimatedLinkComponent
                name="GitHub"
                rounded="rounded-md"
                text="left"
                justify="center"
              />
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="flex flex-col">
      <div>
        <h2>2023 Perry Wang. All Rights Reserved</h2>
      </div>
      <div class="flex flex-row justify-between">
        <p>Made with love and Mango Green Teas (50% sugar, less nice)</p>
        <p>Last updated by Perry on September 16, 2023, 1:27 PM EST</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import AnimatedLinkComponent from '@/components/AnimatedLinkComponent.vue'
</script>
