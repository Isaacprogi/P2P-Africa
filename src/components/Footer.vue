<template>
  <footer class="bg-[#0D4036]  text-white px-4 py-12">
    <div class="max-w-7xl mx-auto">
      <div class="grid md:grid-cols-5 gap-8">
        <!-- Logo and Description -->
        <div class="md:col-span-1">
          <div class="text-3xl font-bold mb-4">
            <img :src="Logo" alt="logo">
          </div>
          <p class="text-teal-300 text-sm leading-relaxed">
           P23 Africa LTD is registered in the United Kingdom. Company No: 15246700
          </p>
        </div>

        <!-- Links Columns -->
        <div  v-for="column in footerColumns" 
          :key="column.title">
            <FooterColumn 
          :title="column.title"
          :links="column.links"
        />
        <div  v-if="column.title === 'Contact Us'" class="flex space-x-3">
          <component 
            v-for="social in socialIcons" 
            :key="social.name"
            :is="social.icon"
            :size="20" 
            class="hover:text-white text-[#CCED60] cursor-pointer transition-colors" 
          />
        </div>
        </div>

        <!-- Newsletter Subscription -->
        <div>
          <h4 class="font-bold mb-4">Subscribe to get Updates</h4>
          <div class="space-y-3">
            <input 
              v-model="email"
              type="email" 
              placeholder="Your email"
              class="w-full px-3 py-2 rounded-lg bg-[#0D4036] text-white placeholder-teal-400 border border-yellow-500 focus:border-teal-500 focus:outline-none"
            />
            <button 
              @click="subscribe"
              class="w-full bg-yellow-400 cursor-pointer text-black px-4 py-2 rounded font-semibold hover:bg-yellow-300 transition-colors"
            >
              Subscribe
            </button>
          </div>
        </div>
      </div>

      <!-- Social Icons and Contact -->
      <div class="mt-8 w-full flex justify-center sm:justify-end items-center">
      <div class=" mt-4 pt-8 text-center text-sm text-teal-400">
        <p>©P23, About and • Privacy Policy • Terms & Conditions</p>
      </div>
        
      </div>

      
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { Facebook, Twitter, Instagram, Linkedin } from 'lucide-vue-next'
import FooterColumn from './FooterColumn.vue'
import Logo from '@/assets/logo.svg'

interface FooterLink {
  name: string
  href: string
}

interface FooterColumnData {
  title: string
  links: FooterLink[]
}

interface SocialIcon {
  name: string
  icon: any
}

const email = ref('')

const footerColumns: FooterColumnData[] = [
  {
    title: 'Who We Are',
    links: [
      { name: 'About Us', href: '#' },
      { name: 'Business Referral Network', href: '#' },
      { name: 'University Partnership', href: '#' },
      { name: 'The 54th Pitch', href: '#' }
    ]
  },
  {
    title: 'What We Do',
    links: [
      { name: 'Business Strategy', href: '#' },
      { name: 'Market Entry', href: '#' },
      { name: 'Business Research', href: '#' },
      { name: 'Sales', href: '#' },
      { name: 'Marketting', href: '#' },
      { name: 'Business Audit', href: '#' }
    ]
  },
  {
    title: 'Contact Us',
    links: []
  }
]

const socialIcons: SocialIcon[] = [
  { name: 'Facebook', icon: Facebook },
  { name: 'Twitter', icon: Twitter },
  { name: 'Instagram', icon: Instagram },
  { name: 'LinkedIn', icon: Linkedin }
]

const subscribe = () => {
  if (email.value) {
    console.log('Subscribing email:', email.value)
    // Add your subscription logic here
    email.value = ''
  }
}
</script>