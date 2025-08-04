<template>
  <div class="relative">
    <div 
      v-for="(profile, index) in profiles" 
      :key="profile.id"
      class="bg-white rounded-xl shadow-lg p-4 max-w-xs absolute"
      :class="profile.positioning"
    >
      <div class="flex items-center space-x-3">
        <img 
          :src="profile.avatar"
          :alt="profile.name" 
          class="w-12 h-12 rounded-full"
        />
        <div>
          <p class="font-semibold text-sm">{{ profile.name }}</p>
          <p class="text-xs text-gray-600">{{ profile.role }}</p>
          <p class="text-xs text-gray-500">{{ profile.expertise }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Profile {
  id: number
  name: string
  role: string
  expertise: string
  avatar: string
  positioning: string
}

const profiles: Profile[] = [
  {
    id: 1,
    name: 'Dr. Amina Thompson',
    role: 'Keynote Speaker',
    expertise: 'Environmental Science Expert',
    avatar: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='50' height='50' viewBox='0 0 50 50'%3E%3Crect width='50' height='50' fill='%23E5E7EB'/%3E%3Ctext x='25' y='30' text-anchor='middle' fill='%23374151' font-size='12'%3EProfile%3C/text%3E%3C/svg%3E",
    positioning: 'transform rotate-2'
  },
  {
    id: 2,
    name: 'Marcus Johnson',
    role: 'Panel Discussion',
    expertise: 'Technology Innovation Leader',
    avatar: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='50' height='50' viewBox='0 0 50 50'%3E%3Crect width='50' height='50' fill='%23E5E7EB'/%3E%3Ctext x='25' y='30' text-anchor='middle' fill='%23374151' font-size='12'%3EProfile%3C/text%3E%3C/svg%3E",
    positioning: 'top-16 left-32 transform -rotate-1'
  }
]
</script>