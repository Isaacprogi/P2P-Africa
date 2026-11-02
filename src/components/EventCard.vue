<template>
  <article :class="[cardClasses, 'group flex flex-col justify-between h-full min-h-[220px]']">
    <div>
      <div class="flex items-start justify-between gap-3 mb-4">
        <div class="flex items-start space-x-3">
          <img
            v-if="event.icon === 'calendar'"
            :src="event.theme === 'dark' ? CalendarDark : CalendarLight"
            class="w-5 h-5 mt-1 shrink-0"
            alt=""
          />
          <MapPin v-else class="w-5 h-5 mt-1 shrink-0 text-teal-700" />

          <h3 :class="titleClasses">{{ event.title }}</h3>
        </div>

        <span v-if="event.isBrb" :class="badgeClasses">BRB</span>
      </div>

      <p :class="descriptionClasses">
        {{ event.description }}
      </p>
    </div>

    <div class="flex items-center space-x-4 mt-6">
      <button :class="primaryButtonClasses">Book A Seat</button>
      <button :class="secondaryButtonClasses">
        <span>{{ detailsButtonText }}</span>
        <ArrowRight :size="14" class="transition-transform duration-200 group-hover:translate-x-0.5" />
      </button>
    </div>
  </article>
</template>

<script setup lang="ts">
import { computed } from "vue";
import { MapPin, ArrowRight } from "lucide-vue-next";
import CalendarDark from "@/assets/calendar-dark.svg";
import CalendarLight from "@/assets/calendar-light.svg";

interface Event {
  id: number;
  title: string;
  description: string;
  theme: "dark" | "light";
  icon: string;
  isBrb?: boolean;
}

const props = defineProps<{ event: Event }>();

const isDark = computed(() => props.event.theme === "dark");

// md:-rotate-[4deg] is a valid arbitrary value (md:-rotate-5 isn't in Tailwind's defaults).
// The tilt straightens on hover; entrance animation lives on the wrapper in Events.vue.
const cardClasses = computed(() =>
  isDark.value
    ? "bg-[#0D4036] rounded-xl shadow-lg p-6 transition-[transform,box-shadow] duration-300 ease-out md:-rotate-[4deg] md:hover:rotate-0 hover:shadow-2xl"
    : "bg-white rounded-xl shadow-lg p-6 transition-[transform,box-shadow] duration-300 ease-out hover:-translate-y-1 hover:shadow-2xl"
);

const titleClasses = computed(() =>
  isDark.value ? "text-white font-bold text-lg leading-snug" : "text-gray-900 font-bold text-lg leading-snug"
);

const descriptionClasses = computed(() =>
  isDark.value
    ? "text-teal-200 text-sm leading-relaxed"
    : "text-gray-600 text-sm leading-relaxed"
);

const badgeClasses = computed(() =>
  isDark.value
    ? "shrink-0 rounded-full bg-[#CCED60] px-2.5 py-0.5 text-xs font-semibold text-[#0D4036]"
    : "shrink-0 rounded-full bg-[#0D4036]/10 px-2.5 py-0.5 text-xs font-semibold text-[#0D4036]"
);

const focusRing =
  "focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#0D4036]";

const primaryButtonClasses = computed(() =>
  isDark.value
    ? `border border-white text-white cursor-pointer px-4 py-2 rounded-lg text-sm transition-colors duration-200 hover:bg-white hover:text-[#0D4036] focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-white`
    : `border border-[#0D4036] text-[#0D4036] cursor-pointer px-4 py-2 rounded-lg text-sm transition-colors duration-200 hover:bg-[#0D4036] hover:text-white ${focusRing}`
);

const secondaryButtonClasses = computed(() =>
  isDark.value
    ? `text-teal-300 py-2 text-sm cursor-pointer hover:text-white flex items-center space-x-1 transition-colors duration-200 ${focusRing}`
    : `text-teal-700 py-2 text-sm cursor-pointer hover:text-teal-900 flex items-center space-x-1 transition-colors duration-200 ${focusRing}`
);

const detailsButtonText = computed(() =>
  props.event.icon === "map-pin" ? "Find Details" : "Event Details"
);
</script>

<style scoped>
@media (prefers-reduced-motion: reduce) {
  article {
    transition: none;
  }
}
</style>