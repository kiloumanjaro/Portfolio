<script setup lang="ts">
import TechnologyComponent from '../TechnologyComponent.vue'
</script>

<template>
  <div class="flex flex-col w-4xl gap-5">
    <h1 class="text-xl px-4">Techstack</h1>
    <div class="grid grid-cols-3 gap-5">
      <TechnologyComponent icon="python" title="Python" width="30%" />
      <TechnologyComponent icon="mdi-language-typescript" title="Typescript" width="30%" />
      <TechnologyComponent icon="mdi-alpha-d-box" title="Django" width="30%" />
      <TechnologyComponent icon="mdi-react" title="React" width="30%" />
      <TechnologyComponent icon="mdi-nodejs" title="NodeJS" width="30%" />
      <TechnologyComponent icon="mdi-language-typescript" title="Typescript" width="30%" />
      <TechnologyComponent icon="mdi-database" title="PostgresSQL" width="30%" />
      <TechnologyComponent icon="mdi-alpha-n-box" title="NextJS" width="30%" />
      <TechnologyComponent icon="mdi-tailwind" title="Tailwind" width="30%" />
    </div>
  </div>
</template>
