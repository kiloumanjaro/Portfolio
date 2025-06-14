<template>
  <div class="flex w-3xl flex-col gap-5">
    <h1 class="text-xl px-4">Projects & Accolades</h1>
    <section>
      <div
        v-for="(project, index) in projects"
        :key="index"
        class="p-4 rounded-xl hover:bg-[#232323] transition-colors w-full"
      >
        <div class="flex flex-row justify-between">
          <div class="flex flex-row gap-2">
            <animated
              :text="project.title"
              class-name="font-bold text-white"
              :delay="index * 300"
            />
            <animated
              :text="project.description"
              class-name="text-gray-400 font-light"
              :delay="index * 300 + 200"
            />
          </div>
          <animated
            :text="project.year"
            tag="span"
            class-name="text-gray-400"
            :delay="index * 300 + 400"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import Animated from '../AnimatedTextComponent.vue'

const projects = [
  {
    title: 'Kids Innovation Camp',
    description: 'Participant',
    year: '2018',
  },
  {
    title: 'Regional Schools Press Conference',
    description: 'Best Layout Design',
    year: '2019',
  },
  {
    title: 'Oblest',
    description: 'Data Structure Project',
    year: '2023',
  },
  {
    title: 'Hackhaton',
    description: 'Participant',
    year: '2024',
  },
  {
    title: 'ThriftNotice',
    description: 'Mobile Application',
    year: '2025',
  },
  {
    title: 'Watchoble',
    description: 'Database Project',
    year: '2025',
  },
  {
    title: 'Road141',
    description: 'Game',
    year: '2025',
  },
]
</script>
