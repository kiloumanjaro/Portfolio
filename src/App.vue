<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import LinkComponent from './components/LinkComponent.vue'
</script>

<template>
  <header>
    <div class="flex flex-row w-full bg-red-600 p-5 justify-between">
      <p>Kilou</p>
      <nav class="flex gap-5">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/info">Info</RouterLink>
      </nav>
      <div class="flex gap-12">
        <LinkComponent
          title="LinkedIn"
          href="https://www.linkedin.com/in/kint-louise-borbano-6982a4327/"
        />
        <LinkComponent title="GitHub" href="https://github.com/kiloumanjaro" />
      </div>
    </div>
  </header>

  <div>
    <RouterView />
  </div>
</template>

<style scoped></style>
