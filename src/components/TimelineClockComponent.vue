<template>
  <div class="p-4 bg-red-600">
    <div class="w-full">
      <div class="items-center min-h-screen">
        <!-- Timeline Wheel -->
        <div class="absolute left-1/2 top-120 transform -translate-x-1/2 -translate-y-1/2">
          <div class="relative w-[2000px] h-[2000px]" ref="constraintsRef">
            <div
              class="absolute inset-0 cursor-grab active:cursor-grabbing transition-transform duration-300 ease-out"
              :style="{ transform: `rotate(${rotation}deg)` }"
              @mousedown="handleMouseDown"
              @touchstart="handleTouchStart"
            >
              <!-- Center circle -->
              <div
                class="absolute top-1/2 left-1/2 w-16 h-16 -translate-x-1/2 -translate-y-1/2 bg-white rounded-full shadow-lg z-10 flex items-center justify-center"
              >
                <div class="w-8 h-8 bg-blue-600 rounded-full"></div>
              </div>

              <!-- Timeline items -->
              <!-- Connection line container -->
              <div
                v-for="(item, index) in timelineData"
                :key="`line-${item.id}`"
                class="absolute"
                :style="{
                  left: `calc(50% + ${getItemPosition(index, lineRadius).x}px)`,
                  top: `calc(50% + ${getItemPosition(index, lineRadius).y}px)`,
                  transform: 'translate(-50%, -50%)',
                }"
              >
                <!-- Connection line to center -->

                <div
                  :class="['absolute w-[1px]', index === selectedIndex ? 'bg-red-600' : 'bg-white']"
                  :style="{
                    height: `30px`,
                    left: '50%',
                    bottom: '-37px',
                    transformOrigin: 'top center',
                    transform: `translateX(-50%) rotate(${getItemAngle(index)}deg)`,
                  }"
                />
              </div>

              <!-- Text container -->
              <div
                v-for="(item, index) in timelineData"
                :key="`text-${item.id}`"
                class="absolute"
                :style="{
                  left: `calc(50% + ${getItemPosition(index, textRadius).x}px)`,
                  top: `calc(50% + ${getItemPosition(index, textRadius).y}px)`,
                  transform: 'translate(-50%, -50%)',
                }"
              >
                <button
                  @click="handleItemClick(index)"
                  class="relative cursor-pointer bg-transparent border-none p-0"
                  :style="{ transform: `rotate(${-rotation}deg)` }"
                >
                  <div
                    :class="[
                      'text-center absolute',
                      index === selectedIndex ? 'text-white' : 'text-[#EBEBEBA3]',
                    ]"
                    style="left: 0px; top: 0px; transform: translate(-50%, -50%)"
                  >
                    <div class="text-lg">{{ item.year }}</div>
                  </div>
                </button>
              </div>

              <!-- Tick marks -->
              <div
                v-for="i in TOTAL_TICKS"
                :key="`tick-${i}`"
                v-show="!isMainItem(i - 1)"
                class="absolute w-[1px] h-4 bg-white"
                :style="{
                  left: `calc(50% + ${getTickPosition(i - 1).x}px)`,
                  top: `calc(50% + ${getTickPosition(i - 1).y}px)`,
                  transform: `translate(-50%, -50%) rotate(${getTickAngle(i - 1)}deg)`,
                  transformOrigin: 'center bottom',
                }"
              />
            </div>
          </div>
        </div>

        <!-- Content Panel -->
        <div class="lg:pl-8">
          <Transition name="slide" mode="out-in">
            <div
              :key="selectedIndex"
              class="bg-white/5 backdrop-blur-lg rounded-2xl p-8 border border-white/10"
            >
              <div class="flex items-center gap-4 mb-6">
                <div class="w-12 h-12 bg-blue-600 rounded-full flex items-center justify-center">
                  <span class="text-white font-bold text-lg">
                    {{ timelineData[selectedIndex].year.toString().slice(-2) }}
                  </span>
                </div>
                <div>
                  <h1 class="text-3xl font-bold text-white">
                    {{ timelineData[selectedIndex].title }}
                  </h1>
                  <p class="text-blue-400 text-lg">{{ timelineData[selectedIndex].year }}</p>
                </div>
              </div>

              <p class="text-xl text-blue-300 mb-6 font-medium">
                {{ timelineData[selectedIndex].description }}
              </p>

              <div class="prose prose-invert max-w-none">
                <p class="text-gray-300 leading-relaxed text-lg">
                  {{ timelineData[selectedIndex].content }}
                </p>
              </div>

              <div class="mt-8 flex gap-4">
                <button
                  class="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition-colors"
                >
                  Learn More
                </button>
                <button
                  class="px-6 py-3 bg-white/10 hover:bg-white/20 text-white rounded-lg font-medium transition-colors backdrop-blur-sm"
                >
                  Share
                </button>
              </div>
            </div>
          </Transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'

interface TimelineItem {
  id: string
  year: number
  title: string
  description: string
  content: string
}

interface Position {
  x: number
  y: number
}

const timelineData: TimelineItem[] = [
  {
    id: 'sketchpad',
    year: 1962,
    title: 'Sketchpad',
    description: 'The first interactive computer graphics program',
    content:
      'Sketchpad was a revolutionary computer program written by Ivan Sutherland in 1963 as part of his PhD thesis. It pioneered the way for human-computer interaction and is considered the ancestor of modern CAD programs and a major breakthrough in the development of computer graphics in general.',
  },
  {
    id: 'mouse',
    year: 1964,
    title: 'Computer Mouse',
    description: "Douglas Engelbart's pointing device invention",
    content:
      'The computer mouse was invented by Douglas Engelbart in 1964 as part of his research into improving human-computer interaction. The first prototype was carved from wood with two metal wheels. This simple device would revolutionize how we interact with computers.',
  },
  {
    id: 'arpanet',
    year: 1969,
    title: 'ARPANET',
    description: 'The precursor to the modern Internet',
    content:
      'ARPANET was the first wide-area network with distributed control and one of the first networks to implement the TCP/IP protocol suite. It was created by the Advanced Research Projects Agency (ARPA) of the United States Department of Defense.',
  },
  {
    id: 'ethernet',
    year: 1973,
    title: 'Ethernet',
    description: 'Local area networking technology',
    content:
      'Ethernet was developed at Xerox PARC by Robert Metcalfe. It became the most widely used LAN technology and is standardized as IEEE 802.3. The original Ethernet operated at 2.94 Mbps and has evolved to support speeds up to 400 Gbps.',
  },
  {
    id: 'personal-computer',
    year: 1975,
    title: 'Personal Computer',
    description: 'The Altair 8800 sparks the PC revolution',
    content:
      'The Altair 8800 was a microcomputer designed in 1974 and based on the Intel 8080 CPU. It sparked the personal computer revolution and inspired many early computer enthusiasts, including Bill Gates and Paul Allen who wrote the first BASIC interpreter for it.',
  },
  {
    id: 'world-wide-web',
    year: 1989,
    title: 'World Wide Web',
    description: "Tim Berners-Lee's information sharing system",
    content:
      'The World Wide Web was invented by Tim Berners-Lee while working at CERN in 1989. He wrote the first web browser, web server, and website. The first website went online in 1991, and by 1993, CERN announced that the Web would be free for everyone to use.',
  },
  {
    id: 'google',
    year: 1996,
    title: 'Google Search',
    description: 'PageRank algorithm revolutionizes web search',
    content:
      'Google began as a research project by Larry Page and Sergey Brin at Stanford University. Their PageRank algorithm revolutionized web search by ranking pages based on their relevance and authority, making it easier to find quality information on the rapidly growing World Wide Web.',
  },
  {
    id: 'iphone',
    year: 2007,
    title: 'iPhone',
    description: 'Smartphone revolution begins',
    content:
      'The iPhone, introduced by Steve Jobs, revolutionized mobile computing by combining a phone, iPod, and internet communicator into one device. Its multi-touch interface and app ecosystem changed how we interact with technology and sparked the mobile app economy.',
  },
]

const selectedIndex = ref(0)
const rotation = ref(0)
const constraintsRef = ref<HTMLElement | null>(null)
const isDragging = ref(false)
const lastPointerPosition = ref({ x: 0, y: 0 })

// Configuration constants
const STARTING_ANGLE = -90 // Aligned to 12 o'clock = 0°
const TOTAL_TICKS = 56 // Use multiple of 4 to align to X and Y axes (0°, 90°, 180°, 270°)
const TICK_ANGLE_STEP = 360 / TOTAL_TICKS // 6° spacing

// Radius configuration
const radius = 200
const textRadius = 240
const lineRadius = 200

// Computed values
const angleStep = computed(() => 360 / timelineData.length)
const itemAngles = computed(() => timelineData.map((_, index) => index * angleStep.value))

// Utility functions
const degreesToRadians = (degrees: number): number => (degrees * Math.PI) / 180

const getPositionFromAngle = (angleDegrees: number, radius: number): Position => {
  const adjustedAngle = angleDegrees + STARTING_ANGLE
  const radians = degreesToRadians(adjustedAngle)
  return {
    x: Math.cos(radians) * radius,
    y: Math.sin(radians) * radius,
  }
}

// Main positioning functions
const getItemPosition = (index: number, customRadius: number = radius): Position => {
  const angle = itemAngles.value[index]
  return getPositionFromAngle(angle, customRadius)
}

const getItemAngle = (index: number): number => {
  return itemAngles.value[index]
}

const getTickPosition = (tickIndex: number): Position => {
  const angle = tickIndex * TICK_ANGLE_STEP + STARTING_ANGLE
  return getPositionFromAngle(angle, radius - 30)
}

const getTickAngle = (tickIndex: number): number => {
  return tickIndex * TICK_ANGLE_STEP + STARTING_ANGLE
}

const isMainItem = (tickIndex: number): boolean => {
  const tickAngle = tickIndex * TICK_ANGLE_STEP
  return itemAngles.value.some(
    (mainAngle) => Math.abs(tickAngle - mainAngle) < 0.5, // Slightly larger tolerance for 56 ticks
  )
}

const handleItemClick = (index: number) => {
  const targetRotation = -index * angleStep.value
  rotation.value = targetRotation
  selectedIndex.value = index
}

const handleMouseDown = (event: MouseEvent) => {
  isDragging.value = true
  lastPointerPosition.value = { x: event.clientX, y: event.clientY }
  document.addEventListener('mousemove', handleMouseMove)
  document.addEventListener('mouseup', handleMouseUp)
}

const handleTouchStart = (event: TouchEvent) => {
  isDragging.value = true
  const touch = event.touches[0]
  lastPointerPosition.value = { x: touch.clientX, y: touch.clientY }
  document.addEventListener('touchmove', handleTouchMove)
  document.addEventListener('touchend', handleTouchEnd)
}

const handleMouseMove = (event: MouseEvent) => {
  if (!isDragging.value) return

  const deltaX = event.clientX - lastPointerPosition.value.x
  const newRotation = rotation.value + deltaX * 0.5
  rotation.value = newRotation
  lastPointerPosition.value = { x: event.clientX, y: event.clientY }

  updateSelectedIndex(newRotation)
}

const handleTouchMove = (event: TouchEvent) => {
  if (!isDragging.value) return

  const touch = event.touches[0]
  const deltaX = touch.clientX - lastPointerPosition.value.x
  const newRotation = rotation.value + deltaX * 0.5
  rotation.value = newRotation
  lastPointerPosition.value = { x: touch.clientX, y: touch.clientY }

  updateSelectedIndex(newRotation)
}

const handleMouseUp = () => {
  isDragging.value = false
  document.removeEventListener('mousemove', handleMouseMove)
  document.removeEventListener('mouseup', handleMouseUp)
}

const handleTouchEnd = () => {
  isDragging.value = false
  document.removeEventListener('touchmove', handleTouchMove)
  document.removeEventListener('touchend', handleTouchEnd)
}

const updateSelectedIndex = (newRotation: number) => {
  const normalizedRotation = ((newRotation % 360) + 360) % 360
  const newIndex = Math.round(normalizedRotation / angleStep.value) % timelineData.length
  selectedIndex.value = newIndex
}

onMounted(() => {
  // Prevent default touch behaviors
  document.addEventListener(
    'touchmove',
    (e) => {
      if (isDragging.value) {
        e.preventDefault()
      }
    },
    { passive: false },
  )
})

onUnmounted(() => {
  document.removeEventListener('mousemove', handleMouseMove)
  document.removeEventListener('mouseup', handleMouseUp)
  document.removeEventListener('touchmove', handleTouchMove)
  document.removeEventListener('touchend', handleTouchEnd)
})
</script>

<style scoped>
.slide-enter-active,
.slide-leave-active {
  transition: all 0.5s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(50px);
}

.slide-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}
</style>
