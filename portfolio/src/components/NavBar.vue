<template>
  <!-- Header & Navigation -->
  <header class="bg-secondary/80 backdrop-blur-md sticky top-0 z-50 shadow-sm">
      <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
                <a href="#" class="text-2xl font-bold text-primary">Your Name</a>
                <div class="hidden md:flex space-x-8">
                    <a v-for="link in navLinks" :key="link.name" :href="link.href" class="text-gray-700 hover:text-primary transition-colors duration-300">{{ link.name }}</a>
                </div>

                <!-- Desktop Links -->
        <div class="hidden md:flex space-x-6 text-gray-700 font-bold">
          <router-link to="/resume" class="hover:text-primary">Resume</router-link>
          <router-link to="/about" class="hover:text-primary">About Me</router-link>
          <router-link to="/projects" class="hover:text-primary">Projects</router-link>
          <router-link to="/" class="hover:text-primary">Blog</router-link>
          <router-link to="/" class="hover:text-primary">Contact Me</router-link>
        </div>

                <!-- Mobile Menu Button -->
                <button @click="mobileMenuOpen = !mobileMenuOpen" class="md:hidden">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
                    </svg>
                </button>
            </nav>
            <!-- Mobile Menu -->
            <div v-show="mobileMenuOpen" class="md:hidden bg-secondary">
                <a v-for="link in navLinks" :key="link.name" :href="link.href" @click="mobileMenuOpen = false" class="block py-2 px-6 text-sm text-gray-700 hover:bg-primary hover:text-secondary transition-colors duration-300">{{ link.name }}</a>
            </div>

            <!-- Mobile Menu -->
      <transition name="fade">
        <div v-if="isOpen" class="md:hidden mt-4 space-y-4 text-center font-bold">
          <router-link to="/" class="block text-gray-700 hover:text-primary">Resume</router-link>
          <router-link to="/about" class="block text-gray-700 hover:text-primary">About Me</router-link>
          <router-link to="/projects" class="block text-gray-700 hover:text-primary">Projects</router-link>
          <router-link to="/blog" class="block text-gray-700 hover:text-primary">Blog</router-link>
          <router-link to="/contact" class="block text-gray-700 hover:text-primary">Contact Me</router-link>
        </div>
      </transition>
        </header>
</template>

<script setup>
import { ref } from 'vue'

  const isOpen = ref(false)
  const toggleMenu = () => {
    isOpen.value = !isOpen.value
  }
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: all 0.3s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

</style>
