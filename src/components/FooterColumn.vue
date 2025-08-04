<!-- components/FooterColumn.vue -->
<template>
  <div>
    <h4 class="font-bold mb-4">{{ title }}</h4>
    <ul v-if="links.length > 0" class="space-y-2 text-sm text-teal-300">
      <li v-for="link in links" :key="link.name">
        <a 
          :href="link.href" 
          class="hover:text-white transition-colors"
        >
          {{ link.name }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
interface FooterLink {
  name: string
  href: string
}

interface Props {
  title: string
  links: FooterLink[]
}

defineProps<Props>()
</script>