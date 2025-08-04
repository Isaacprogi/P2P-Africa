<!-- components/EventCard.vue -->
<template>
  <div :class="cardClasses">
    <div class="flex items-start space-x-3 mb-4">
      <component 
        :is="iconComponent" 
        :class="iconClasses"
        :size="20" 
      />
      <div>
        <h3 :class="titleClasses">{{ event.title }}</h3>
      </div>
    </div>
    <p :class="descriptionClasses">
      {{ event.description }}
    </p>
    <div class="flex space-x-4">
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

const iconComponent = computed(() => {
  return props.event.icon === 'calendar' ? Calendar : MapPin
})

const cardClasses = computed(() => {
  return props.event.theme === 'dark' 
    ? 'bg-[#0D4036] rounded-xl shadow-lg md:-rotate-5 p-6'
    : 'bg-white shadow-lg rounded-xl p-6'
})

const iconClasses = computed(() => {
  return props.event.theme === 'dark' ? 'text-teal-300  mt-1' : 'text-teal-700 mt-1'
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
    ? 'border border-white hover:bg-[#2E6258] cursor-pointer  rounded-lg text-white px-4 py-2 rounded text-sm  transition-colors'
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