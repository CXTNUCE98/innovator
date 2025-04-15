<script lang="ts" setup>
import Logo from "@/public/logo.png"

const menuItems = [
  {
    title: 'Trang chủ',
    to: '/'
  },
  {
    title: 'Giới thiệu',
    to: '/introduce'
  },
  {
    title: 'Đội ngũ chuyên gia',
    to: '/teamofexperts'
  },
  {
    title: 'Bài viết',
    to: '/article'
  },
  {
    title: 'Dịch vụ',
    to: '/service'
  },
  {
    title: 'Liên hệ',
    to: '/contact'
  },
]

// Simple state for menu toggle
const isMenuOpen = ref(false)
function toogleMenu() {
  isMenuOpen.value = true
}

function handleActiveMenu() {
    console.log('running');
    isMenuOpen.value = false
}
</script>

<template>
  <header class="bg-white shadow-sm fixed w-full top-0 z-50">
    <div class="container mx-auto px-4 flex items-center justify-between h-16">
      <!-- Mobile Menu Button -->
      <button @click="toogleMenu" class="md:hidden focus:outline-none">
        <svg v-if="!isMenuOpen" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
          stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
        <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
          stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
      <!-- Logo -->
      <div class="flex items-center">
        <NuxtLink to="/" class="flex items-center">
          <img :src="Logo" alt="Innovator Academy" class="h-40px md:h-80px object-cover" />
        </NuxtLink>
      </div>

      <div class="block md:hidden"></div>

      <!-- Desktop Navigation -->
      <nav class="hidden md:flex items-center space-x-8">
        <template v-for="item in menuItems" :key="item.to">
          <NuxtLink :to="item.to" class="nav-link">{{ item.title }}</NuxtLink>
        </template>
      </nav>

      <!-- CTA Button -->
      <div class="hidden md:block">
        <button class="bg-yellow-500 hover:bg-yellow-600 text-white py-2 px-4 rounded-md transition-colors duration-300">
          Nhận tư vấn
        </button>
      </div>


    </div>

    <!-- Mobile Menu (always in DOM, visible based on state) -->
    <div class="fixed top-0 left-0 h-full w-full bg-white shadow-lg z-50 md:hidden transition-transform duration-300"
      :class="isMenuOpen ? 'translate-x-0' : '-translate-x-full'">
      <div class="flex justify-between items-center p-4 border-b">
        <div class="flex gap-2">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
          <span class="font-medium">Menu</span>
        </div>
        <button @click="isMenuOpen = false" class="focus:outline-none">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <nav>
        <ul>
          <template v-for="item in menuItems" :key="item.to">
            <li class="border-b" @click="handleActiveMenu">
              <NuxtLink :to="item.to" class=" px-4 py-5 hover:bg-gray-100 flex justify-between items-center">
                {{ item.title }}
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                </svg>
              </NuxtLink>
            </li>
          </template>
        </ul>
      </nav>
    </div>

    <!-- Mobile Menu Overlay - Click to Close -->
    <div v-if="isMenuOpen" class="fixed inset-0 bg-black bg-opacity-30 z-40 md:hidden" @click="isMenuOpen = false"></div>
  </header>
</template>



<style scoped>
.nav-link {
  @apply text-gray-700 hover:text-yellow-500 font-medium transition-colors duration-300;
}

.nav-link.router-link-active {
  @apply text-yellow-500 bg-[#FFFBF1] px-4 py-2 rounded-lg;
}
</style>