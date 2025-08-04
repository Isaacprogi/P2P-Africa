<!-- components/GeometricShapes.vue -->
<template>
  <div class="relative">
    <div class="grid grid-cols-3 gap-4 max-w-md">
      <!-- Row 1 -->
      <div class="bg-teal-300 rounded-full w-20 h-20"></div>
      <div class="bg-orange-500 rounded-full w-20 h-20"></div>
      <div class="bg-yellow-400 rounded-full w-20 h-20"></div>
      
      <!-- Row 2 -->
      <div class="bg-teal-800 rounded-3xl w-20 h-32"></div>
      <div class="bg-orange-500 rounded-3xl w-20 h-32 relative overflow-hidden">
        <div class="absolute inset-0 bg-white opacity-20">
          <svg class="w-full h-full" viewBox="0 0 20 32">
            <defs>
              <pattern id="zigzag" patternUnits="userSpaceOnUse" width="4" height="4">
                <path d="M0,2 L2,0 L4,2 L2,4 Z" fill="white" opacity="0.3"/>
              </pattern>
            </defs>
            <rect width="20" height="32" fill="url(#zigzag)"/>
          </svg>
        </div>
      </div>
      <div class="bg-teal-800 rounded-3xl w-20 h-32"></div>
      
      <!-- Row 3 -->
      <div class="bg-orange-500 rounded-full w-20 h-20"></div>
      <div class="bg-teal-300 rounded-3xl w-20 h-24"></div>
      <div class="bg-purple-300 rounded-2xl w-20 h-20 flex items-center justify-center">
        <span class="text-white font-bold text-lg">isaac</span>
      </div>
    </div>
    
    <!-- Bottom decorative shapes -->
    <div class="absolute -bottom-8 left-0">
      <div class="bg-orange-400 rounded-full w-16 h-16 relative overflow-hidden">
        <svg class="absolute inset-0 w-full h-full" viewBox="0 0 16 16">
          <path d="M8,2 Q12,6 8,10 Q4,6 8,2" fill="white" opacity="0.3"/>
        </svg>
      </div>
    </div>
    <div class="absolute -bottom-4 left-20">
      <div class="bg-purple-200 rounded-2xl w-12 h-16 relative overflow-hidden">
        <svg class="absolute inset-0 w-full h-full" viewBox="0 0 12 16">
          <circle cx="6" cy="4" r="2" fill="white" opacity="0.4"/>
          <circle cx="6" cy="12" r="2" fill="white" opacity="0.4"/>
        </svg>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// No additional logic needed for this component
</script>