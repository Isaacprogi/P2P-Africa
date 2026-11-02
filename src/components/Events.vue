<template>
  <section
    ref="sectionRef"
    :style="`background-image: url(${RectangleGreenBackground})`"
    class="bg-teal-700 relative overflow-hidden py-16 md:py-24"
  >
    <div class="max-w-[1400px] z-10 mx-auto">
      <div class="grid md:grid-cols-3 md:gap-8">
        <!-- Mobile intro -->
        <div class="text-white px-4 md:hidden col-span-full">
          <h2 class="text-2xl font-bold mb-4">Upcoming Event For This Year</h2>
          <p class="text-teal-200 mb-6 text-sm leading-relaxed max-w-prose">
            Explore upcoming events tailored to equip, connect, and empower
            businesses across Africa and beyond.
          </p>
          <button class="see-all">
            <span>See All Events</span>
            <ArrowRight :size="16" class="arrow" />
          </button>
        </div>

        <!-- Mobile tabs -->
        <div class="md:hidden bg-white col-span-full pt-6 mt-6">
          <div
            role="tablist"
            class="flex items-center justify-between border-b-2 border-black"
          >
            <button
              v-for="tab in tabs"
              :key="tab.id"
              role="tab"
              :aria-selected="activeTab === tab.id"
              @click="activeTab = tab.id"
              :class="[
                'tab text-sm flex-1 py-4 font-semibold',
                activeTab === tab.id ? 'text-white bg-[#0D4036]' : 'text-[#0D4036]',
              ]"
            >
              {{ tab.label }}
            </button>
          </div>
        </div>

        <!-- Cards -->
        <div
          :class="[
            'grid md:grid-cols-2 lg:grid-cols-3 gap-6 col-span-full px-4 pt-6 bg-white md:bg-transparent',
            { 'is-in': revealed },
          ]"
        >
          <!-- Desktop intro -->
          <div class="text-white hidden md:block col-span-full md:col-span-1">
            <h2 class="text-3xl font-bold mb-4 leading-tight">
              Upcoming Event For This Year
            </h2>
            <p class="text-teal-200 mb-6 text-sm leading-relaxed max-w-prose">
              Explore upcoming events focused on topics like technology,
              business innovation, and personal development. Join us for
              meaningful conversations and networking opportunities.
            </p>
            <button class="see-all">
              <span>See All Events</span>
              <ArrowRight :size="16" class="arrow" />
            </button>
          </div>

          <!--
            The wrapper owns the entrance animation (opacity + translate).
            The card inside owns its own transform (the dark card's tilt),
            so the two never fight over `transform`.
          -->
          <div
            v-for="(event, i) in visibleEvents"
            :key="event.id"
            class="card-item"
            :style="{ '--i': i }"
          >
            <EventCard :event="event" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount } from "vue";
import { ArrowRight } from "lucide-vue-next";
import EventCard from "./EventCard.vue";
import RectangleGreenBackground from "@/assets/rectangle-green-background.svg";

interface Event {
  id: number;
  title: string;
  description: string;
  theme: "dark" | "light";
  icon: string;
  isBrb: boolean;
}

type TabId = "event" | "brb";

const tabs: { id: TabId; label: string }[] = [
  { id: "event", label: "Events" },
  { id: "brb", label: "BRB" },
];

const allEvents: Event[] = [
  {
    id: 1,
    title: "Tech Conference",
    description:
      "Join industry leaders and innovators as they explore the future of artificial intelligence, web development, and cloud computing in this immersive 3-day event.",
    theme: "dark",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 2,
    title: "BRB Coffee Break",
    description:
      "Take a well-deserved pause to recharge, network casually with peers, and enjoy locally brewed coffee in our cozy breakout lounge.",
    theme: "light",
    icon: "calendar",
    isBrb: true,
  },
  {
    id: 3,
    title: "Marketing Masterclass",
    description:
      "An in-depth workshop on emerging digital marketing trends, personalized advertising, and social media strategy for 2025.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 4,
    title: "Design Thinking Bootcamp",
    description:
      "Experience a hands-on session focused on solving real-world problems using the design thinking methodology—ideal for designers, product managers, and startup founders.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 5,
    title: "BRB Power Nap Pod",
    description:
      "Feeling drained? Visit our power nap pods to rest, reset, and regain your energy for the rest of the day’s activities.",
    theme: "light",
    icon: "calendar",
    isBrb: true,
  },
  {
    id: 6,
    title: "Next-Gen Startups Panel",
    description:
      "Hear from the founders of disruptive startups in fintech, healthtech, and edtech as they share their journeys, challenges, and visions for the future.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 7,
    title: "BRB Social Mixer",
    description:
      "Unwind and mingle with fellow attendees over drinks and live acoustic music in a relaxed, informal setting.",
    theme: "light",
    icon: "calendar",
    isBrb: true,
  },
  {
    id: 8,
    title: "Frontend Frameworks Showdown",
    description:
      "A live debate between advocates of React, Vue, and Svelte. See real-world use cases, performance benchmarks, and community perspectives.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
];

const activeTab = ref<TabId>("event");

// matchMedia fires only when the breakpoint is crossed,
// unlike a resize listener which fires on every pixel.
const isDesktop = ref(true);
let media: MediaQueryList | null = null;
const onMediaChange = (e: MediaQueryListEvent) => (isDesktop.value = e.matches);

// Reveal cards once the section scrolls into view.
const sectionRef = ref<HTMLElement | null>(null);
const revealed = ref(false);
let observer: IntersectionObserver | null = null;

onMounted(() => {
  media = window.matchMedia("(min-width: 768px)");
  isDesktop.value = media.matches;
  media.addEventListener("change", onMediaChange);

  if (!("IntersectionObserver" in window) || !sectionRef.value) {
    revealed.value = true;
    return;
  }
  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        revealed.value = true;
        observer?.disconnect();
      }
    },
    { threshold: 0.15 }
  );
  observer.observe(sectionRef.value);
});

onBeforeUnmount(() => {
  media?.removeEventListener("change", onMediaChange);
  observer?.disconnect();
});

const visibleEvents = computed(() => {
  if (isDesktop.value || activeTab.value === "event") return allEvents;
  return allEvents.filter((e) => e.isBrb);
});
</script>

<style scoped>
/* Cards: hidden until the section is in view, then a short stagger. */
.card-item {
  opacity: 0;
}

.is-in .card-item {
  animation: card-rise 0.6s cubic-bezier(0.22, 1, 0.36, 1) both;
  animation-delay: calc(var(--i, 0) * 70ms);
}

@keyframes card-rise {
  from {
    opacity: 0;
    transform: translate3d(0, 24px, 0);
  }
  to {
    opacity: 1;
    transform: none;
  }
}

/* Buttons */
.see-all {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: #fff;
  color: #0f766e;
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  font-weight: 600;
  font-size: 0.875rem;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.2s ease;
}
.see-all:hover {
  background: #f3f4f6;
}
.see-all:hover .arrow {
  transform: translateX(3px);
}
.see-all:focus-visible,
.tab:focus-visible {
  outline: 2px solid #ccED60;
  outline-offset: 2px;
}
.arrow {
  transition: transform 0.2s ease;
}

.tab {
  transition: background-color 0.2s ease, color 0.2s ease;
}

@media (prefers-reduced-motion: reduce) {
  .card-item {
    opacity: 1;
  }
  .is-in .card-item {
    animation: none;
  }
  .arrow,
  .tab,
  .see-all {
    transition: none;
  }
}
</style>