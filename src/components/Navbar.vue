<!-- components/Navbar.vue -->
<template>
  <header class="bg-[#0D4036] flex items-center text-white px-4 h-[85px] py-3">
    <div class="max-w-7xl mx-auto w-full flex items-center justify-between">
      <div class="flex items-center space-x-8">
        <img :src="Logo" alt="Logo" >
        <nav class="hidden md:flex space-x-6 text-sm">
          <a 
            v-for="item in navItems" 
            :key="item.name"
            :href="item.href" 
            class="hover:text-teal-200 transition-colors"
          >
            {{ item.name }}
          </a>
        </nav>
      </div>
      
      <div class="flex items-center space-x-4">
        <button class="border px-4 py-2 rounded-lg border-white/50 text-sm transition-colors">
          Subscribe
        </button>
        <div class="flex space-x-2">
          <component 
            v-for="social in socialIcons" 
            :key="social.name"
            :is="social.icon"
            :size="20" 
            class="hover:text-teal-200 cursor-pointer transition-colors" 
          />
        </div>
      </div>
    </div>
  </header>
</template>

<script setup lang="ts">
import { Facebook, Twitter, Instagram, Linkedin } from 'lucide-vue-next'
import Logo from '@/assets/logo.svg'

interface NavItem {
  name: string
  href: string
}

interface SocialIcon {
  name: string
  icon: any
}

const navItems: NavItem[] = [
  { name: 'Who we are', href: '#' },
  { name: 'What We Do', href: '#' },
  { name: 'Our Events', href: '#' },
  { name: 'Resources hub', href: '#' },
  { name: "Let's collaborate", href: '#' }
]

const socialIcons: SocialIcon[] = [
  { name: 'Facebook', icon: Facebook },
  { name: 'Twitter', icon: Twitter },
  { name: 'Instagram', icon: Instagram },
  { name: 'LinkedIn', icon: Linkedin }
]
</script>