<template>
  <section
    :style="`background-image: url(${RectangleGreenBackground})`"
    class="bg-teal-700 relative overflow-hidden px-4 py-16"
  >
    <div class="max-w-7xl z-10 mx-auto">
      <!-- Grid Layout -->
      <div class="grid md:grid-cols-3 gap-8">

          <div class="text-white md:hidden col-span-full md:col-span-1">
          <h2 class="text-2xl font-bold mb-4">Upcoming Event For This Year</h2>
          <p class="text-teal-200 mb-6 text-sm leading-relaxed">
            Explore upcoming events focused on topics like technology, business innovation, and personal development. Join us for meaningful conversations and networking opportunities.
          </p>
          <button class="bg-white text-teal-700 px-6 py-3 rounded-lg font-semibold text-sm hover:bg-gray-100 flex items-center space-x-2 transition-colors">
            <span>See All Events</span>
            <ArrowRight :size="16" />
          </button>
        </div>
        <!-- Tabs for Small Screens -->
        <div class="md:hidden col-span-full mt-6">
          <div class="flex gap-4 border-b border-teal-500 pb-2">
            <button
              @click="activeTab = 'featured'"
              :class="[
                'text-sm font-semibold',
                activeTab === 'featured' ? 'text-white border-b-2 border-white' : 'text-teal-200'
              ]"
            >
              Featured
            </button>
            <button
              @click="activeTab = 'regular'"
              :class="[
                'text-sm font-semibold',
                activeTab === 'regular' ? 'text-white border-b-2 border-white' : 'text-teal-200'
              ]"
            >
              Regular
            </button>
          </div>
        </div>

        <!-- Featured Events (Shown in Tabs on small screens, always on md+) -->
        <div
          v-if="activeTab === 'featured' || windowWidth >= 768"
          class="grid md:grid-cols-2 lg:grid-cols-3 gap-6 col-span-full mt-6"
        >
        <div class="text-white hidden md:block col-span-full md:col-span-1">
          <h2 class="text-2xl font-bold mb-4">Upcoming Event For This Year</h2>
          <p class="text-teal-200 mb-6 text-sm leading-relaxed">
            Explore upcoming events focused on topics like technology, business innovation, and personal development. Join us for meaningful conversations and networking opportunities.
          </p>
          <button class="bg-white text-teal-700 px-6 py-3 rounded-lg font-semibold text-sm hover:bg-gray-100 flex items-center space-x-2 transition-colors">
            <span>See All Events</span>
            <ArrowRight :size="16" />
          </button>
        </div>
          <EventCard
            v-for="event in featuredEvents"
            :key="event.id"
            :event="event"
          />
        </div>

        <!-- Regular Events (Shown in Tabs on small screens, always on md+) -->
        <div
          v-if="activeTab === 'regular' || windowWidth >= 768"
          class="grid md:grid-cols-2 lg:grid-cols-3 gap-6 col-span-full mt-6"
        >
          <EventCard
            v-for="event in regularEvents"
            :key="event.id"
            :event="event"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { ArrowRight } from 'lucide-vue-next'
import EventCard from './EventCard.vue'
import RectangleGreenBackground from '@/assets/rectangle-green-background.svg'

interface Event {
  id: number
  title: string
  description: string
  theme: 'dark' | 'light'
  icon: string
}

// Sample event data
const featuredEvents: Event[] = [
  {
    id: 1,
    title: 'Vision & Execution',
    description: 'Explore the latest developments and insights in strategic planning, innovative solutions, and successful project implementation across various industries.',
    theme: 'dark',
    icon: 'calendar'
  },
  {
    id: 2,
    title: 'Event Home',
    description: 'Explore event details and join us for inspiring conversations, network with industry experts, and access valuable resources for professional growth.',
    theme: 'light',
    icon: 'map-pin'
  }
]

const regularEvents: Event[] = [
  {
    id: 3,
    title: 'Event Name',
    description: 'Join us for this comprehensive discussion with experts and thought leaders as we explore relevant topics and industry trends.',
    theme: 'light',
    icon: 'calendar'
  },
  {
    id: 4,
    title: 'Event Name',
    description: 'Join us for this comprehensive discussion with experts and thought leaders as we explore relevant topics and industry trends.',
    theme: 'light',
    icon: 'calendar'
  },
  {
    id: 5,
    title: 'Event Name',
    description: 'Join us for this comprehensive discussion with experts and thought leaders as we explore relevant topics and industry trends.',
    theme: 'light',
    icon: 'calendar'
  }
]

// Tab state
const activeTab = ref<'featured' | 'regular'>('featured')

// Track window width to control responsive behavior
const windowWidth = ref(window.innerWidth)

const handleResize = () => {
  windowWidth.value = window.innerWidth
}

onMounted(() => {
  window.addEventListener('resize', handleResize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)
})
</script>
