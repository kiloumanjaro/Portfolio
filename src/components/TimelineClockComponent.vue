<template>
  <!-- p-4 * 4.5 = 72px -->
  <div class="absolute top-0 left-0 w-full">
    <div class="">
      <!-- Timeline Wheel -->
      <div class="scale-110">
        <!-- top-120 * 4.5 = 540px -->
        <div style="width: 2000px; height: 1950px" ref="constraintsRef">
          <!-- 2000px * 4.5 = 9000px -->
          <div
            class="absolute inset-0 cursor-grab active:cursor-grabbing transition-transform duration-300 ease-out"
            :style="{ transform: `rotate(${rotation}deg)` }"
            @mousedown="handleMouseDown"
            @touchstart="handleTouchStart"
            @mousemove="handleMouseMove"
            @mouseup="handleMouseUp"
            @mouseleave="handleMouseUp"
            @touchmove="handleTouchMove"
            @touchend="handleTouchEnd"
          >
            <!-- Timeline items -->
            <!-- Connection line container -->
            <div
              v-for="(item, index) in timelineData"
              :key="`line-${item.id}`"
              class="absolute"
              :style="{
                left: `calc(50% + ${getItemPosition(index, lineRadius).x}px)`,
                top: `calc(49.2% + ${getItemPosition(index, lineRadius).y}px)`,
              }"
            >
              <!-- Connection line to center -->
              <div
                :class="['absolute', index === selectedIndex ? 'bg-red-600' : 'bg-gray-400']"
                :style="{
                  width: '1.5px',
                  height: '55px',
                  left: '50%',
                  bottom: '-70.5px',
                  transformOrigin: 'top center',
                  transform: `translateX(-50%) rotate(${getItemAngle(index)}deg)`,
                }"
              />
              <!-- 1px * 4.5 = 4.5px, 30px * 4.5 = 135px, -37px * 4.5 = -166.5px -->
            </div>

            <!-- Text container -->
            <div
              v-for="(item, index) in timelineData"
              :key="`text-${item.id}`"
              class="absolute"
              :style="{
                left: `calc(50% + ${getItemPosition(index, textRadius).x}px)`,
                top: `calc(49.2% + ${getItemPosition(index, textRadius).y}px)`,
                transform: 'translate(-50%)',
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
                  :style="{
                    left: '0px',
                    top: '0px',
                    transform: 'translate(-50%, -50%)',
                    fontSize: '15px',
                  }"
                >
                  <!-- text-lg * 4.5 = 81px -->
                  {{ item.year }}
                </div>
              </button>
            </div>

            <!-- Tick marks -->
            <div
              v-for="i in TOTAL_TICKS"
              :key="`tick-${i}`"
              v-show="!isMainItem(i - 1)"
              class="absolute bg-gray-400/70"
              :style="{
                width: '1px',
                height: '30px',
                left: `calc(50% + ${getTickPosition(i - 1).x}px)`,
                top: `calc(49.2% + ${getTickPosition(i - 1).y}px)`,
                transform: `translate(-50%, -50%) rotate(${getTickAngle(i - 1)}deg)`,
                transformOrigin: 'center bottom',
              }"
            />
            <!-- 1px * 4.5 = 4.5px, 4px * 4.5 = 18px -->
          </div>
        </div>
        <!-- Fixed Center circle - outside rotating container -->
        <div
          class="absolute top-1/2 left-1/2 bg-white rounded-full shadow-lg z-10 flex items-center justify-center"
          style="width: 72px; height: 72px; transform: translate(-50%, -50%)"
        >
          <!-- 16px * 4.5 = 72px -->
          <div class="bg-blue-600 rounded-full" style="width: 36px; height: 36px"></div>
          <!-- 8px * 4.5 = 36px -->
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'

interface TimelineItem {
  id: string
  year: string
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
    year: '1962',
    title: 'Sketchpad',
    description: 'The first interactive computer graphics program',
    content:
      'Sketchpad was a revolutionary computer program written by Ivan Sutherland in 1963 as part of his PhD thesis. It pioneered the way for human-computer interaction and is considered the ancestor of modern CAD programs and a major breakthrough in the development of computer graphics in general.',
  },
  {
    id: 'mouse',
    year: '1964',
    title: 'Computer Mouse',
    description: "Douglas Engelbart's pointing device invention",
    content:
      'The computer mouse was invented by Douglas Engelbart in 1964 as part of his research into improving human-computer interaction. The first prototype was carved from wood with two metal wheels. This simple device would revolutionize how we interact with computers.',
  },
  {
    id: 'arpanet',
    year: '  1969',
    title: 'ARPANET',
    description: 'The precursor to the modern Internet',
    content:
      'ARPANET was the first wide-area network with distributed control and one of the first networks to implement the TCP/IP protocol suite. It was created by the Advanced Research Projects Agency (ARPA) of the United States Department of Defense.',
  },
  {
    id: 'ethernet',
    year: '   1973',
    title: 'Ethernet',
    description: 'Local area networking technology',
    content:
      'Ethernet was developed at Xerox PARC by Robert Metcalfe. It became the most widely used LAN technology and is standardized as IEEE 802.3. The original Ethernet operated at 2.94 Mbps and has evolved to support speeds up to 400 Gbps.',
  },
  {
    id: 'personal-computer',
    year: '    1975',
    title: 'Personal Computer',
    description: 'The Altair 8800 sparks the PC revolution',
    content:
      'The Altair 8800 was a microcomputer designed in 1974 and based on the Intel 8080 CPU. It sparked the personal computer revolution and inspired many early computer enthusiasts, including Bill Gates and Paul Allen who wrote the first BASIC interpreter for it.',
  },
  {
    id: 'world-wide-web',
    year: '    1989    ',
    title: 'World Wide Web',
    description: "Tim Berners-Lee's information sharing system",
    content:
      'The World Wide Web was invented by Tim Berners-Lee while working at CERN in 1989. He wrote the first web browser, web server, and website. The first website went online in 1991, and by 1993, CERN announced that the Web would be free for everyone to use.',
  },
  {
    id: 'google',
    year: '1996',
    title: 'Google Search',
    description: 'PageRank algorithm revolutionizes web search',
    content:
      'Google began as a research project by Larry Page and Sergey Brin at Stanford University. Their PageRank algorithm revolutionized web search by ranking pages based on their relevance and authority, making it easier to find quality information on the rapidly growing World Wide Web.',
  },
  {
    id: 'iphone',
    year: '2007',
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
const lastAngle = ref(0)

// Configuration constants
const STARTING_ANGLE = -90 // Aligned to 12 o'clock = 0°
const TOTAL_TICKS = 88 // Use multiple of 4 to align to X and Y axes (0°, 90°, 180°, 270°)
const TICK_ANGLE_STEP = 360 / TOTAL_TICKS // 6° spacing

// Radius configuration - all scaled by 4.5x
const radius = 900 // 200 * 4.5
const textRadius = 840 // 240 * 4.5
const lineRadius = 815 // 200 * 4.5

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

// Simplified angle calculation from center point
const getAngleFromEvent = (clientX: number, clientY: number): number => {
  if (!constraintsRef.value) return 0

  const rect = constraintsRef.value.getBoundingClientRect()
  const centerX = rect.left + rect.width / 2
  const centerY = rect.top + rect.height / 2
  const x = clientX - centerX
  const y = clientY - centerY
  return Math.atan2(y, x) * (180 / Math.PI)
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
  return getPositionFromAngle(angle, radius - 135) // 30 * 4.5 = 135
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

// Simplified drag handlers using the cleaner physics approach
const handleMouseDown = (event: MouseEvent) => {
  if (!isDragging.value) {
    isDragging.value = true
    lastAngle.value = getAngleFromEvent(event.clientX, event.clientY)
    event.preventDefault()
  }
}

const handleTouchStart = (event: TouchEvent) => {
  if (!isDragging.value) {
    isDragging.value = true
    const touch = event.touches[0]
    lastAngle.value = getAngleFromEvent(touch.clientX, touch.clientY)
    event.preventDefault()
  }
}

const handleMouseMove = (event: MouseEvent) => {
  if (!isDragging.value) return

  const currentAngle = getAngleFromEvent(event.clientX, event.clientY)
  let angleDiff = currentAngle - lastAngle.value

  // Handle angle wrap-around
  if (angleDiff > 180) angleDiff -= 360
  if (angleDiff < -180) angleDiff += 360

  rotation.value += angleDiff
  lastAngle.value = currentAngle

  updateSelectedIndex(rotation.value)
}

const handleTouchMove = (event: TouchEvent) => {
  if (!isDragging.value) return

  const touch = event.touches[0]
  const currentAngle = getAngleFromEvent(touch.clientX, touch.clientY)
  let angleDiff = currentAngle - lastAngle.value

  // Handle angle wrap-around
  if (angleDiff > 180) angleDiff -= 360
  if (angleDiff < -180) angleDiff += 360

  rotation.value += angleDiff
  lastAngle.value = currentAngle

  updateSelectedIndex(rotation.value)
}

const handleMouseUp = () => {
  isDragging.value = false
}

const handleTouchEnd = () => {
  isDragging.value = false
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
  // Cleanup is handled by Vue's event system since we moved to inline handlers
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
