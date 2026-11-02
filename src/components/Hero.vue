<template>
  <section class="bg-white px-4 py-16 md:py-24 overflow-hidden">
    <div class="max-w-[1400px] mx-auto">
      <div class="grid md:grid-cols-2 gap-10 md:gap-16 items-center">
        <!-- Left: geometric shapes (desktop only) -->
        <div class="hidden md:block hero-shapes">
          <img :src="shapesDesktop" alt="" class="w-full h-auto" />
        </div>

        <!-- Right: content -->
        <div class="space-y-8 md:space-y-10">
          <h1
            class="hero-title text-center md:text-left text-4xl sm:text-5xl md:text-6xl font-bold text-gray-900 leading-[1.1] tracking-tight"
          >
            Gaining Knowledge<br />
            <span class="text-gray-500 font-normal">Through Connection.</span>
          </h1>

          <div class="hero-people">
            <img :src="peopleDesktop" alt="" class="hidden md:block w-full h-auto" />
            <img :src="peopleMobile" alt="" class="md:hidden w-full h-auto" />
          </div>

          <img :src="shapesMobile" alt="" class="hero-shapes-mobile md:hidden w-full h-auto" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import shapesDesktop from "@/assets/shapes-dectop.svg";
import peopleDesktop from "@/assets/people-dectop.svg";
import shapesMobile from "@/assets/shapes-mobile.svg";
import peopleMobile from "@/assets/people-mobile.svg";
</script>

<style scoped>
/*
  One orchestrated entrance on page load.
  Small distances (24px, not 100%) so nothing sweeps in from off-screen
  and the page never gets a horizontal scrollbar flash.
*/
@keyframes rise {
  from {
    opacity: 0;
    transform: translate3d(0, 20px, 0);
  }
  to {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

@keyframes drift-in {
  from {
    opacity: 0;
    transform: translate3d(-24px, 0, 0);
  }
  to {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

.hero-title,
.hero-people,
.hero-shapes,
.hero-shapes-mobile {
  animation-duration: 0.8s;
  animation-timing-function: cubic-bezier(0.22, 1, 0.36, 1);
  animation-fill-mode: both;
}

.hero-shapes {
  animation-name: drift-in;
}
.hero-title {
  animation-name: rise;
  animation-delay: 0.1s;
}
.hero-people {
  animation-name: rise;
  animation-delay: 0.25s;
}
.hero-shapes-mobile {
  animation-name: rise;
  animation-delay: 0.4s;
}

@media (prefers-reduced-motion: reduce) {
  .hero-title,
  .hero-people,
  .hero-shapes,
  .hero-shapes-mobile {
    animation: none;
  }
}
</style>