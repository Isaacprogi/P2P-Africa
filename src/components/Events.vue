<template>
  <section
    :style="`background-image: url(${RectangleGreenBackground})`"
    class="bg-teal-700 relative overflow-hidden  py-16"
  >
    <div class="max-w-[1400px]  z-10 mx-auto">
      <!-- Grid Layout -->
      <div class="grid md:grid-cols-3 md:gap-8">
        <div class="text-white px-4 md:hidden col-span-full md:col-span-1">
          <h2 class="text-2xl font-bold mb-4">Upcoming Event For This Year</h2>
          <p class="text-teal-200 mb-6 text-sm leading-relaxed">
            Explore upcoming events tailored to equip, 
            connect, and empower businesses across Africa and beyond.
          </p>
          <button
            class="bg-white text-teal-700 px-6 py-3 rounded-lg font-semibold text-sm hover:bg-gray-100 flex items-center space-x-2 transition-colors"
          >
            <span>See All Events</span>
            <ArrowRight :size="16" />
          </button>
        </div>
        <!-- Tabs for Small Screens -->
        <div class="md:hidden bg-white md:bg-none col-span-full pt-6 mt-6">
          <div class="flex items-center justify-between gap-4 border-b-2 border-black">
            <button
              @click="activeTab = 'event'"
              :class="[
                'text-sm flex-1 py-4 font-semibold',
                activeTab === 'event'
                  ? 'text-white bg-[#0D4036]'
                  : 'text-[#0D4036]',
              ]"
            >
              Events
            </button>
            <button
              @click="activeTab = 'brb'"
              :class="[
                'text-sm flex-1 py-4 font-semibold',
                activeTab === 'brb'
                  ? 'text-white  bg-[#0D4036]'
                  : 'text-[#0D4036]',
              ]"
            >
              BRB
            </button>
          </div>
        </div>

        <!-- Featured Events (Shown in Tabs on small screens, always on md+) -->
        <div
          
          class="grid md:grid-cols-2 px-4 bg-white md:bg-transparent lg:grid-cols-3 gap-6 col-span-full pt-6"
        >
          <div class="text-white hidden md:block col-span-full md:col-span-1">
            <h2 class="text-2xl font-bold mb-4">
              Upcoming Event For This Year
            </h2>
            <p class="text-teal-200 mb-6 text-sm leading-relaxed">
              Explore upcoming events focused on topics like technology,
              business innovation, and personal development. Join us for
              meaningful conversations and networking opportunities.
            </p>
            <button
              class="bg-white text-teal-700 px-6 py-3 rounded-lg font-semibold text-sm hover:bg-gray-100 flex items-center space-x-2 transition-colors"
            >
              <span>See All Events</span>
              <ArrowRight :size="16" />
            </button>
          </div>

          <EventCard
            v-for="event in filteredEvents"
            :key="event.id"
            :event="event"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount,computed } from "vue";
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

const allEvents: Event[] = [
  {
    id: 1,
    title: "Tech Conference",
    description: "Join industry leaders and innovators as they explore the future of artificial intelligence, web development, and cloud computing in this immersive 3-day event.",
    theme: "dark",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 2,
    title: "BRB Coffee Break",
    description: "Take a well-deserved pause to recharge, network casually with peers, and enjoy locally brewed coffee in our cozy breakout lounge.",
    theme: "light",
    icon: "calendar",
    isBrb: true,
  },
  {
    id: 3,
    title: "Marketing Masterclass",
    description: "An in-depth workshop on emerging digital marketing trends, personalized advertising, and social media strategy for 2025.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 4,
    title: "Design Thinking Bootcamp",
    description: "Experience a hands-on session focused on solving real-world problems using the design thinking methodology—ideal for designers, product managers, and startup founders.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 5,
    title: "BRB Power Nap Pod",
    description: "Feeling drained? Visit our power nap pods to rest, reset, and regain your energy for the rest of the day’s activities.",
    theme: "light",
    icon: "calendar",
    isBrb: true,
  },
  {
    id: 6,
    title: "Next-Gen Startups Panel",
    description: "Hear from the founders of disruptive startups in fintech, healthtech, and edtech as they share their journeys, challenges, and visions for the future.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
  {
    id: 7,
    title: "BRB Social Mixer",
    description: "Unwind and mingle with fellow attendees over drinks and live acoustic music in a relaxed, informal setting.",
    theme: "light",
    icon: "calendar",
    isBrb: true,
  },
  {
    id: 8,
    title: "Frontend Frameworks Showdown",
    description: "A live debate between advocates of React, Vue, and Svelte. See real-world use cases, performance benchmarks, and community perspectives.",
    theme: "light",
    icon: "calendar",
    isBrb: false,
  },
];


// Tab state
const activeTab = ref<"event" | "brb">("event");

// Track window width to control responsive behavior
const windowWidth = ref(window.innerWidth);

const handleResize = () => {
  windowWidth.value = window.innerWidth;
};

onMounted(() => {
  window.addEventListener("resize", handleResize);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", handleResize);
});

const filteredEvents = computed(() => {
  if (windowWidth.value >= 768) return allEvents;
  return activeTab.value === "event"
    ? allEvents
    : allEvents.filter((event) => event.isBrb);
});
</script>
