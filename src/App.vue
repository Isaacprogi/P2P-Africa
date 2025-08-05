<template>
  <div class="min-h-screen bg-gray-50">
    <Navbar />
    <HeroSection />
    <EventsSection />
    <FooterSection />
  </div>
</template>

<script setup lang="ts">
import Navbar from './components/Navbar.vue'
import HeroSection from './components/Hero.vue'
import EventsSection from './components/Events.vue'
import FooterSection from './components/Footer.vue'
</script>