<script setup lang="ts">
import { RouterView } from 'vue-router'
import LinkComponent from './components/LinkComponent.vue'
import TabsComponent from './components/TabsComponent.vue'
</script>

<template>
  <header>
    <div class="flex flex-row w-full p-10 justify-between items-center">
      <h1 class="text-lg font-bold">KILOU</h1>
      <div class="flex gap-12">
        <LinkComponent
          title="LinkedIn"
          href="https://www.linkedin.com/in/kint-louise-borbano-6982a4327/"
        />
        <LinkComponent title="GitHub" href="https://github.com/kiloumanjaro" />
      </div>
      <div class="absolute left-1/2 transform -translate-x-1/2">
        <TabsComponent />
      </div>
    </div>
  </header>

  <div>
    <RouterView />
  </div>
</template>

<style scoped></style>
