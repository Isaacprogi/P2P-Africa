<template>
  <div>
    <header
      class="bg-[#0D4036] flex items-center text-white px-4 h-[85px] py-3 relative z-50"
    >
      <div class="max-w-[1400px] mx-auto w-full flex items-center justify-between">
        <div class="flex items-center space-x-8">
          <img :src="Logo" alt="Logo" />

          <!-- Navigation -->
          <nav class="hidden md:flex space-x-6 text-sm relative" aria-label="Main">
            <!-- First 3 items always visible -->
            <a
              v-for="item in navItems.slice(0, 3)"
              :key="item.name"
              :href="item.href"
              class="nav-link"
            >
              {{ item.name }}
            </a>

            <!-- "More" dropdown (md only) -->
            <div ref="moreRef" class="relative lg:hidden">
              <button
                class="nav-link cursor-pointer"
                aria-haspopup="true"
                :aria-expanded="showMore"
                @click="showMore = !showMore"
              >
                More
                <span class="chevron" :class="{ open: showMore }" aria-hidden="true">▾</span>
              </button>

              <Transition name="menu">
                <div
                  v-if="showMore"
                  class="absolute left-0 mt-3 w-48 bg-white text-black shadow-xl rounded-lg overflow-hidden z-50 origin-top-left"
                >
                  <a
                    v-for="item in navItems.slice(3)"
                    :key="item.name"
                    :href="item.href"
                    class="block px-4 py-2.5 hover:bg-teal-50 transition-colors"
                    @click="showMore = false"
                  >
                    {{ item.name }}
                  </a>
                </div>
              </Transition>
            </div>

            <!-- Remaining items at lg+ -->
            <a
              v-for="item in navItems.slice(3)"
              :key="item.name"
              :href="item.href"
              class="nav-link hidden lg:inline"
            >
              {{ item.name }}
            </a>
          </nav>
        </div>

        <!-- Hamburger (mobile) -->
        <button
          class="md:hidden cursor-pointer rounded p-1 focus-visible:outline-2 focus-visible:outline-[#CCED60]"
          aria-label="Open menu"
          @click="isSidebarOpen = true"
        >
          <img :src="Menu" alt="" />
        </button>

        <!-- Right side -->
        <div class="hidden md:flex items-center space-x-4">
          <button
            class="border border-white hover:bg-white hover:text-[#0D4036] w-[112px] h-[44px] flex items-center justify-center cursor-pointer rounded-lg text-white px-4 py-2 text-sm transition-colors duration-200 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#CCED60]"
          >
            Subscribe
          </button>
          <div class="flex space-x-4">
            <img
              v-for="social in socialIcons"
              :key="social.name"
              :src="social.icon"
              class="w-5 h-5 cursor-pointer opacity-100 hover:opacity-80 hover:-translate-y-0.5 transition duration-200"
              :alt="social.name"
            />
          </div>
        </div>
      </div>
    </header>

    <!-- Mobile drawer: backdrop fades, panel slides (separately, so the backdrop never slides) -->
    <Transition name="fade">
      <div
        v-if="isSidebarOpen"
        class="fixed inset-0 bg-black/50 z-[80]"
        aria-hidden="true"
        @click="isSidebarOpen = false"
      />
    </Transition>

    <Transition name="drawer">
      <aside
        v-if="isSidebarOpen"
        class="fixed left-0 top-0 h-full w-64 bg-[#0D4036] shadow-2xl p-6 z-[90] overflow-y-auto"
        role="dialog"
        aria-modal="true"
        aria-label="Menu"
      >
        <div class="flex justify-between items-center mb-8">
          <img :src="Logo" alt="Logo" class="h-8" />
          <button
            class="text-white/80 hover:text-white text-xl leading-none p-1 cursor-pointer transition-colors focus-visible:outline-2 focus-visible:outline-[#CCED60]"
            aria-label="Close menu"
            @click="isSidebarOpen = false"
          >
            ✕
          </button>
        </div>

        <nav class="flex flex-col space-y-5" aria-label="Mobile">
          <a
            v-for="item in navItems"
            :key="item.name"
            :href="item.href"
            class="text-white/90 hover:text-[#CCED60] transition-colors"
            @click="isSidebarOpen = false"
          >
            {{ item.name }}
          </a>
        </nav>

        <div class="mt-8 flex space-x-4">
          <img
            v-for="social in socialIcons"
            :key="social.name"
            :src="social.icon"
            class="w-5 h-5 cursor-pointer hover:opacity-80 transition-opacity duration-200"
            :alt="social.name"
          />
        </div>
      </aside>
    </Transition>
  </div>
</template>

<script setup lang="ts">
import { ref, watch, onMounted, onBeforeUnmount } from "vue";
import Logo from "@/assets/Logo.svg";
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
const moreRef = ref<HTMLElement | null>(null);

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

// Close the "More" dropdown on outside click.
const onDocClick = (e: MouseEvent) => {
  if (showMore.value && moreRef.value && !moreRef.value.contains(e.target as Node)) {
    showMore.value = false;
  }
};

// Escape closes whichever menu is open.
const onKeydown = (e: KeyboardEvent) => {
  if (e.key === "Escape") {
    showMore.value = false;
    isSidebarOpen.value = false;
  }
};

// Stop the page scrolling behind the open drawer.
watch(isSidebarOpen, (open) => {
  document.body.style.overflow = open ? "hidden" : "";
});

onMounted(() => {
  document.addEventListener("click", onDocClick);
  document.addEventListener("keydown", onKeydown);
});

onBeforeUnmount(() => {
  document.removeEventListener("click", onDocClick);
  document.removeEventListener("keydown", onKeydown);
  document.body.style.overflow = "";
});
</script>

<style scoped>
/* Nav links: underline grows from the left on hover/focus. */
.nav-link {
  position: relative;
  padding-bottom: 2px;
  transition: color 0.2s ease;
}
.nav-link::after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  bottom: -2px;
  height: 2px;
  background: #ccED60;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.25s ease;
}
.nav-link:hover,
.nav-link:focus-visible {
  color: #ccED60;
}
.nav-link:hover::after,
.nav-link:focus-visible::after {
  transform: scaleX(1);
}
.nav-link:focus-visible {
  outline: none;
}

.chevron {
  display: inline-block;
  transition: transform 0.2s ease;
}
.chevron.open {
  transform: rotate(180deg);
}

/* Dropdown */
.menu-enter-active,
.menu-leave-active {
  transition: opacity 0.18s ease, transform 0.18s ease;
}
.menu-enter-from,
.menu-leave-to {
  opacity: 0;
  transform: translateY(-6px) scale(0.98);
}

/* Backdrop */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Drawer panel */
.drawer-enter-active,
.drawer-leave-active {
  transition: transform 0.35s cubic-bezier(0.22, 1, 0.36, 1);
}
.drawer-enter-from,
.drawer-leave-to {
  transform: translateX(-100%);
}

@media (prefers-reduced-motion: reduce) {
  .nav-link::after,
  .chevron,
  .menu-enter-active,
  .menu-leave-active,
  .fade-enter-active,
  .fade-leave-active,
  .drawer-enter-active,
  .drawer-leave-active {
    transition-duration: 0.01ms;
  }
}
</style>