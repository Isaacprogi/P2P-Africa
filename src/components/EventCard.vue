<template>
  <div :class="[cardClasses, 'flex flex-col justify-between min-h-[220px]']">
    <div>
      <div class="flex items-start space-x-3 mb-4">
        <template v-if="props.event.icon === 'calendar'">
          <img
            :src="props.event.theme === 'dark' ? CalendarDark : CalendarLight"
            class="w-5 h-5 mt-1"
            :alt="event.title"
          />
        </template>
        <template v-else>
          <MapPin class="w-5 h-5 mt-1 text-teal-700" />
        </template>

        <div>
          <h3 :class="titleClasses">{{ event.title }}</h3>
        </div>
      </div>

      <p :class="descriptionClasses">
        {{ event.description }}
      </p>
    </div>

    <!-- Buttons always at bottom -->
    <div class="flex space-x-4 mt-6">
      <button :class="primaryButtonClasses">
        Book A Seat
      </button>
      <button :class="secondaryButtonClasses">
        <span>{{ detailsButtonText }}</span>
        <ArrowRight :size="14" />
      </button>
    </div>
  </div>
</template>


<script setup lang="ts">
import { computed } from 'vue'
import { Calendar, MapPin, ArrowRight } from 'lucide-vue-next'
import CalendarDark from '@/assets/calendar-dark.svg'
import CalendarLight from '@/assets/calendar-light.svg'

interface Event {
  id: number
  title: string
  description: string
  theme: 'dark' | 'light'
  icon: string
}

interface Props {
  event: Event
}

const props = defineProps<Props>()


const cardClasses = computed(() => {
  return props.event.theme === 'dark' 
    ? 'bg-[#0D4036] rounded-xl shadow-lg md:-rotate-5 p-6'
    : 'bg-white shadow-lg rounded-xl p-6'
})


const titleClasses = computed(() => {
  return props.event.theme === 'dark' 
    ? 'text-white font-bold text-lg'
    : 'text-gray-900 font-bold text-lg'
})

const descriptionClasses = computed(() => {
  return props.event.theme === 'dark' 
    ? 'text-teal-200 text-sm mb-6 leading-relaxed'
    : 'text-gray-600 text-sm mb-6 leading-relaxed'
})

const primaryButtonClasses = computed(() => {
  return props.event.theme === 'dark'
    ? 'border border-white hover:bg-[#1B3A36] cursor-pointer  rounded-lg text-white px-4 py-2 rounded text-sm  transition-colors'
    : 'border border-[#0D4036] text-[#0D4036] cursor-pointer px-4 py-2 rounded-lg text-sm hover:bg-gray-100 transition-colors'
})

const secondaryButtonClasses = computed(() => {
  return props.event.theme === 'dark'
    ? 'text-teal-300 px-4 py-2 text-sm cursor-pointer hover:text-white flex items-center space-x-1 transition-colors'
    : 'text-teal-700 px-4 py-2 text-sm cursor-pointer hover:text-teal-800 flex items-center space-x-1 transition-colors'
})

const detailsButtonText = computed(() => {
  return props.event.icon === 'map-pin' ? 'Find Details' : 'Event Details'
})
</script>