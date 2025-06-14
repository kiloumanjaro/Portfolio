<template>
  <div class="flex w-3xl flex-col gap-5">
    <h1 class="text-xl px-4">Contacts</h1>
    <section>
      <div
        v-for="(information, index) in informations"
        :key="index"
        class="p-4 rounded-xl transition-colors w-full"
      >
        <div class="flex flex-row justify-between">
          <a
            v-if="information.url"
            :href="information.url"
            target="_blank"
            rel="noopener noreferrer"
            class="text-lg text-white hover:text-blue-500 transition-colors"
          >
            <animated :text="information.contact" class-name="" :delay="index * 300" />
          </a>
          <span v-else class="text-lg text-white">
            <animated :text="information.contact" class-name="" :delay="index * 300" />
          </span>
          <animated
            :text="information.type"
            class-name="text-sm text-gray-400"
            :delay="index * 300 + 200"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import Animated from '../AnimatedTextComponent.vue'

const informations = [
  {
    contact: 'kiloumanjaro@gmail.com',
    type: 'Email Address',
    url: 'mailto:kiloumanjaro@gmail.com',
  },
  {
    contact: 'read.cv/kilou',
    type: 'read.cv',
  },
  {
    contact: 'linkedin.com/in/kiloumanjaro/',
    type: 'LinkedIn',
    url: 'https://linkedin.com/in/kiloumanjaro/',
  },
  {
    contact: 'github.com/kiloumanjaro',
    type: 'GitHub',
    url: 'https://github.com/kiloumanjaro',
  },
  {
    contact: 'My Resume',
    type: 'PDF',
    url: 'https://docs.google.com/document/d/1ma9JwQVPzg0UafmtfNk4JpLgX9s-qQA-CEJVvuNcOQ8/edit?usp=sharing',
  },
  {
    contact: 'Design Portfolio',
    type: 'Behance',
    url: 'https://behance.net/KintB',
  },
  {
    contact: 'Editing Portfolio',
    type: 'YouTube',
    url: 'https://youtube.com/c/ORIKA', // Update to actual URL
  },
]
</script>
