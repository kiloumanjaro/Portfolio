<template>
  <div class="flex items-center justify-center">
    <div class="bg-[#232323] rounded-full p-1 flex">
      <RouterLink to="/">
        <button
          @click="activeTab = 'work'"
          :class="[
            'px-6 py-2 rounded-full text-sm transition-all duration-200',
            activeTab === 'work' ? 'bg-[#333333] text-white' : 'text-gray-400 hover:text-gray-300',
          ]"
        >
          Work
        </button>
      </RouterLink>

      <RouterLink to="/info">
        <button
          @click="activeTab = 'info'"
          :class="[
            'px-6 py-2 rounded-full text-sm transition-all duration-200',
            activeTab === 'info' ? 'bg-[#333333] text-white' : 'text-gray-400 hover:text-gray-300',
          ]"
        >
          Info
        </button>
      </RouterLink>
    </div>
  </div>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { ref } from 'vue'
const activeTab = ref('work')
</script>
