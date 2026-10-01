<template>
  <header class="site-header">
    <div class="container header-inner">
      <button class="brand" type="button" @click="$emit('change-view', 'home')">
        <span class="brand-mark">MA</span>
        <span>Melbourne AutoHub</span>
      </button>

      <nav class="main-nav" aria-label="Main navigation">
        <button
          v-for="item in navItems"
          :key="item.id"
          type="button"
          :class="{ active: activeView === item.id }"
          @click="$emit('change-view', item.id)"
        >
          {{ item.label }}
        </button>
      </nav>
    </div>
  </header>
</template>

<script setup>
defineProps({
  activeView: {
    type: String,
    default: 'home'
  }
})

defineEmits(['change-view'])

const navItems = [
  { id: 'home', label: 'Home' },
  { id: 'cars', label: 'Cars' },
  { id: 'contact', label: 'Contact / Test Drive' }
]
</script>
