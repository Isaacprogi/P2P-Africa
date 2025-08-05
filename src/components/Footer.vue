<template>
  <footer class="bg-[#0D4036] text-white px-4 py-12">
    <div class=" max-w-[400px] md:max-w-[1400px]  mx-auto">
      <div class="grid md:grid-cols-5 gap-8">

        <!-- Logo and Description -->
        <div class="md:col-span-1 flex gap-2 justify-between">
          <div class="flex flex-col">
            <div class="text-3xl font-bold mb-4">
            <img :src="Logo" alt="logo" />
          </div>
          <p class="text-teal-300 max-w-[13rem] sm:max-w-full text-sm leading-relaxed">
            P23 Africa LTD is registered in the United Kingdom. Company No:
            15246700
          </p>
          </div>

          <div class="md:hidden">
              <h1 class="mb-5">Quick Links</h1>
              <div>
                <ul class="text-teal-300 flex flex-col gap-2 text-sm">
                  <li v-for="link in quickLinks" :key="link.name">
                    <a :href="link.href" class="hover:text-white font-[500]  transition-colors">
                      {{ link.name }}
                    </a>
                  </li>
                </ul>
              </div>
          </div>
        </div>

        <!-- Links Columns -->
        
        <div  class="hidden md:block" v-for="column in footerColumns" :key="column.title">
          <FooterColumn :title="column.title" :links="column.links" />
          <div v-if="column.title === 'Contact Us'" class="flex space-x-3">
              <img
              v-for="social in socialIcons"
              :key="social.name"
              :src="social.icon"
              class="hover:opacity-[0.8] duration-300 w-5 h-5 cursor-pointer transition-opacity"
              :alt="social.name"
            />
          </div>
        </div>

        <div class="md:hidden">
          <h4 class="font-bold mb-5">Subscribe to get Updates</h4>
          <div class="space-y-3 bg-white max-w-[256px] h-[56px] rounded-lg overflow-hidden flex">
            <input
              v-model="email"
              type="email"
              placeholder="Your email"
              class="w-full px-3 flex-1 h-full b py-2 rounded-lg text-[#0D4036]"
            />
            <button
              @click="subscribe"
              class=" bg-[#CCED60] flex-none min-w-[24px] cursor-pointer text-black px-4 py-2 rounded font-semibold hover:bg-yellow-300 transition-colors"
            >
               <ArrowRight/>
            </button>
          </div>
        </div>

        <div  class="md:hidden" v-for="column in [footerColumns[2]]" :key="column.title">
          <FooterColumn :title="column.title" :links="column.links" />
          <div v-if="column.title === 'Contact Us'" class="flex space-x-3">
              <img
              v-for="social in socialIcons"
              :key="social.name"
              :src="social.icon"
              class="hover:opacity-[0.8] duration-300 w-5 h-5 cursor-pointer transition-opacity"
              :alt="social.name"
            />
          </div>
        </div>

        <!-- Newsletter Subscription -->
        <div class="hidden md:block">
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
              class="w-full bg-[#CCED60] flex gap-2 items-center justify-center cursor-pointer text-black px-4 py-2 rounded-lg font-semibold hover:bg-yellow-300 transition-colors"
            >
              Subscribe
              <ArrowRight/>
            </button>
          </div>
        </div>
      </div>

      <!-- terms -->
      <div class="mt-8 w-full  flex justify-end items-center">
        <div class="mt-4 pt-8 terms flex items-center  text-right  text-sm text-white">
          <p>©P23 Africa 2025<div class="hidden md:inline"> •  About and • Privacy Policy • Terms & Conditions</div></p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref } from "vue";
import FooterColumn from "./FooterColumn.vue";
import Logo from "@/assets/Logo.svg";
import Facebook from "@/assets/facebook-yellow.svg";
import Linkedin from "@/assets/linkedin-yellow.svg";
import Instagram from "@/assets/instagram-yellow.svg";
import Youtube from "@/assets/youtube-yellow.svg";
import { ArrowRight } from "lucide-vue-next";

interface FooterLink {
  name: string;
  href: string;
}

interface FooterColumnData {
  title: string;
  links: FooterLink[];
}

interface SocialIcon {
  name: string;
  icon: any;
}

const email = ref("");

const footerColumns: FooterColumnData[] = [
  {
    title: "Who We Are",
    links: [
      { name: "About Us", href: "#" },
      { name: "Business Referral Network", href: "#" },
      { name: "University Partnership", href: "#" },
      { name: "The 54th Pitch", href: "#" },
    ],
  },
  {
    title: "What We Do",
    links: [
      { name: "Business Strategy", href: "#" },
      { name: "Market Entry", href: "#" },
      { name: "Business Research", href: "#" },
      { name: "Sales", href: "#" },
      { name: "Marketting", href: "#" },
      { name: "Business Audit", href: "#" },
    ],
  },
  {
    title: "Contact Us",
    links: [],
  },
];

const quickLinks =  [
      { name: "Business Strategy", href: "#" },
      { name: "Market Entry", href: "#" },
      { name: "Business Research", href: "#" },
      { name: "Sales", href: "#" },
      { name: "Marketting", href: "#" },
      { name: "Business Audit", href: "#" },
    ]

const socialIcons: SocialIcon[] = [
    { name: "LinkedIn", icon: Linkedin },
  { name: "Facebook", icon: Facebook },
  { name: "Instagram", icon: Instagram },
  { name: "Youtube", icon: Youtube },
];

const subscribe = () => {
  if (email.value) {
    console.log("Subscribing email:", email.value);
    // Add your subscription logic here
    email.value = "";
  }
};
</script>
