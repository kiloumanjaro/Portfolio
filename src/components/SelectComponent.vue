<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import { ChevronDown, Check } from 'lucide-vue-next'

// Props
const props = defineProps({
  options: {
    type: Array,
    default: () => [
      { value: 'option1', label: 'Option 1' },
      { value: 'option2', label: 'Option 2' },
      { value: 'option3', label: 'Option 3' },
      { value: 'option4', label: 'Option 4' },
    ],
  },
  placeholder: {
    type: String,
    default: 'Select an option',
  },
  modelValue: {
    type: [String, Number, Object],
    default: null,
  },
})

// Emits
const emit = defineEmits(['update:modelValue'])

// Reactive state
const isOpen = ref(false)
const selectRef = ref(null)

// Computed
const selectedOption = ref(props.modelValue)
const displayText = ref(props.placeholder)

// Methods
const toggleDropdown = () => {
  isOpen.value = !isOpen.value
}

const selectOption = (option) => {
  selectedOption.value = option.value
  displayText.value = option.label
  isOpen.value = false
  emit('update:modelValue', option.value)
}

const closeDropdown = () => {
  isOpen.value = false
}

// Click outside handler
const handleClickOutside = (event) => {
  if (selectRef.value && !selectRef.value.contains(event.target)) {
    closeDropdown()
  }
}

// Keyboard navigation
const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeDropdown()
  }
}

// Lifecycle
onMounted(() => {
  document.addEventListener('click', handleClickOutside)
  document.addEventListener('keydown', handleKeydown)

  // Set initial display text if modelValue is provided
  if (props.modelValue) {
    const initialOption = props.options.find((option) => option.value === props.modelValue)
    if (initialOption) {
      displayText.value = initialOption.label
      selectedOption.value = initialOption.value
    }
  }
})

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside)
  document.removeEventListener('keydown', handleKeydown)
})
</script>

<template>
  <div class="relative inline-block w-64" ref="selectRef">
    <!-- Select Button -->
    <button
      @click="toggleDropdown"
      class="w-full px-4 py-3 text-left bg-white border border-gray-300 rounded-lg shadow-sm hover:border-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-colors duration-200"
      :class="{ 'border-blue-500 ring-2 ring-blue-500': isOpen }"
    >
      <div class="flex items-center justify-between">
        <span
          class="block truncate"
          :class="{ 'text-gray-500': !selectedOption, 'text-gray-900': selectedOption }"
        >
          {{ displayText }}
        </span>
        <ChevronDown
          class="w-5 h-5 text-gray-400 transition-transform duration-200"
          :class="{ 'rotate-180': isOpen }"
        />
      </div>
    </button>

    <!-- Dropdown Options -->
    <Transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="transform scale-95 opacity-0"
      enter-to-class="transform scale-100 opacity-100"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="transform scale-100 opacity-100"
      leave-to-class="transform scale-95 opacity-0"
    >
      <div
        v-if="isOpen"
        class="absolute z-10 w-full mt-1 bg-white border border-gray-300 rounded-lg shadow-lg max-h-60 overflow-auto"
      >
        <ul class="py-1">
          <li
            v-for="option in options"
            :key="option.value"
            @click="selectOption(option)"
            class="px-4 py-3 cursor-pointer hover:bg-gray-50 flex items-center justify-between transition-colors duration-150"
            :class="{ 'bg-blue-50 text-blue-600': selectedOption === option.value }"
          >
            <span class="block truncate">{{ option.label }}</span>
            <Check v-if="selectedOption === option.value" class="w-4 h-4 text-blue-600" />
          </li>
        </ul>
      </div>
    </Transition>
  </div>

  <!-- Demo Section -->
  <div class="mt-8 p-6 bg-gray-50 rounded-lg">
    <h3 class="text-lg font-semibold mb-4">Demo</h3>
    <div class="space-y-4">
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-2">
          Choose your favorite framework:
        </label>
        <div class="relative inline-block w-64">
          <button
            @click="isOpen = !isOpen"
            class="w-full px-4 py-3 text-left bg-white border border-gray-300 rounded-lg shadow-sm hover:border-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-colors duration-200"
          >
            <div class="flex items-center justify-between">
              <span class="block truncate text-gray-900">
                {{
                  selectedOption
                    ? options.find((opt) => opt.value === selectedOption)?.label
                    : placeholder
                }}
              </span>
              <ChevronDown class="w-5 h-5 text-gray-400" />
            </div>
          </button>
        </div>
      </div>

      <div v-if="selectedOption" class="p-3 bg-green-50 border border-green-200 rounded-lg">
        <p class="text-sm text-green-800">
          <strong>Selected:</strong>
          {{ options.find((opt) => opt.value === selectedOption)?.label }}
        </p>
        <p class="text-xs text-green-600 mt-1"><strong>Value:</strong> {{ selectedOption }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Additional custom styles if needed */
.rotate-180 {
  transform: rotate(180deg);
}
</style>
