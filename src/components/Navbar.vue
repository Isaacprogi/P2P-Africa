<template>
  <div>
    <!-- Header -->
    <header
      class="bg-[#0D4036] flex items-center text-white px-4 h-[85px] py-3 relative z-50"
    >
      <div class="max-w-[1400px] mx-auto w-full flex items-center justify-between">
        <div class="flex items-center space-x-8">
          <img :src="Logo" alt="Logo" />

          <!-- Navigation -->
          <nav class="hidden md:flex space-x-6 text-sm relative">
            <!-- Always show first 3 items -->
            <template
              v-for="(item, index) in navItems.slice(0, 3)"
              :key="item.name"
            >
              <a
                :href="item.href"
                class="hover:text-teal-200 transition-colors"
              >
                {{ item.name }}
              </a>
            </template>

            <!-- More dropdown (only for md) -->
            <div class="relative group lg:hidden">
              <button
                @click="showMore = !showMore"
                class="hover:text-teal-200 cursor-pointer transition-colors"
              >
                More ▾
              </button>
              <div
                v-if="showMore"
                class="absolute left-0 mt-2 w-48 bg-white text-black shadow-lg rounded group-hover:block z-50"
              >
                <template v-for="item in navItems.slice(3)" :key="item.name">
                  <a
                    :href="item.href"
                    class="block px-4 py-2 hover:bg-teal-100"
                  >
                    {{ item.name }}
                  </a>
                </template>
              </div>
            </div>

            <!-- Show all items at lg+ -->
            <template v-for="item in navItems.slice(3)" :key="item.name">
              <a
                :href="item.href"
                class="hidden lg:inline hover:text-teal-200 transition-colors"
              >
                {{ item.name }}
              </a>
            </template>
          </nav>
        </div>

        <!-- Hamburger Menu for Mobile -->
        <img :src="Menu" alt="Menu" class="md:hidden cursor-pointer" @click="isSidebarOpen = true">

        <!-- Right Side: Subscribe & Social Icons -->
        <div class="hidden md:flex items-center space-x-4">
          <button
            class="border border-white hover:bg-[#1B3A36] w-[112px] h-[44px] flex items-center justify-center cursor-pointer  rounded-lg text-white px-4 py-2 text-sm  transition-all"
          >
            Subscribe
          </button>
          <div class="flex space-x-4">
            <img
              v-for="social in socialIcons"
              :key="social.name"
              :src="social.icon"
              class="hover:opacity-[0.8] duration-300 w-5 h-5 cursor-pointer transition-opacity"
              :alt="social.name"
            />
          </div>
        </div>
      </div>
    </header>

    <!-- Sidebar for Mobile -->
    <transition name="slide">
      <div
        v-if="isSidebarOpen"
        class="fixed inset-0 bg-black/50 z-80"
        @click.self="isSidebarOpen = false"
      >
        <aside
          class="w-64 bg-[#0D4036] h-full shadow-lg p-6 absolute left-0 top-0 z-50"
        >
          <div class="flex justify-between items-center mb-6">
            <img :src="Logo" alt="Logo" class="h-8" />
            <button
              @click="isSidebarOpen = false"
              class="text-white hover:text-gray-700"
            >
              ✕
            </button>
          </div>
          <nav class="flex flex-col space-y-4">
            <template v-for="item in navItems" :key="item.name">
              <a :href="item.href" class="text-white hover:text-teal-600">
                {{ item.name }}
              </a>
            </template>
          </nav>
          <div class="mt-8 flex space-x-4">
             <img
              v-for="social in socialIcons"
              :key="social.name"
              :src="social.icon"
              class="hover:opacity-[0.8] duration-300 w-5 h-5 cursor-pointer transition-opacity"
              :alt="social.name"
            />
          </div>
        </aside>
      </div>
    </transition>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import Logo from "@/assets/logo.svg";
import Facebook from "@/assets/facebook.svg";
import Linkedin from "@/assets/linkedin.svg";
import Instagram from "@/assets/instagram.svg";
import Youtube from "@/assets/youtube.svg";
import Menu from "@/assets/Menu.svg";

interface NavItem {
  name: string;
  href: string;
}

interface SocialIcon {
  name: string;
  icon: any;
}

const isSidebarOpen = ref(false);
const showMore = ref(false);

const navItems: NavItem[] = [
  { name: "Who we are", href: "#" },
  { name: "What We Do", href: "#" },
  { name: "Our Events", href: "#" },
  { name: "Resources hub", href: "#" },
  { name: "Let's collaborate", href: "#" },
];

const socialIcons: SocialIcon[] = [
  { name: "LinkedIn", icon: Linkedin },
  { name: "Facebook", icon: Facebook },
  { name: "Instagram", icon: Instagram },
  { name: "Youtube", icon: Youtube },
];
</script>

<style scoped>
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s ease;
}
.slide-enter-from {
  transform: translateX(-100%);
}
.slide-enter-to {
  transform: translateX(0);
}
.slide-leave-from {
  transform: translateX(0);
}
.slide-leave-to {
  transform: translateX(-100%);
}
</style>
