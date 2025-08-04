<!-- components/HeroSection.vue -->
<template>
  <section class="bg-white px-4 py-16">
    <div class="max-w-7xl mx-auto">
      <div class="grid md:grid-cols-2 gap-12 items-center">
        <!-- Left Side - Geometric Shapes -->
        <img  class="hidden md:block" :src="shapesDextop" alt="">
        
        <!-- Right Side - Content -->
        <div class="space-y-8">
          <div class="text-center md:text-left">
            <h1 class="text-5xl md:text-6xl font-bold text-gray-900 leading-tight">
              Gaining Knowledge<br />
              <span class="text-gray-600 font-normal">Through Connection.</span>
            </h1>
          </div>
          <img class="hidden md:flex" :src="peopleDextop" alt="">
          <div class="w-full">
            <img class="md:hidden w-full " :src="peopleMobile" alt=""></img>
          </div>
          <div class="md:hidden flex w-full items-center justify-between">
            <img class="w-full" :src="shapesMobile" alt=""></img>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import shapesDextop from '@/assets/shapes-dectop.svg';
import peopleDextop from '@/assets/people-dectop.svg';
import shapesMobile from '@/assets/shapes-mobile.svg';
import peopleMobile from '@/assets/people-mobile.svg';
</script>