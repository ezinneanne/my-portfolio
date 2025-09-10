<template>
  <!-- Header & Navigation -->
  <header class="bg-secondary/80 backdrop-blur-md sticky top-0 z-50 shadow-sm">
    <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
      <p class="text-2xl font-bold text-primary">Ezinne Anne Emilia</p>

      <!-- Desktop Links -->
      <div class="hidden md:flex space-x-8 text-gray-700 font-bold">
        <router-link to="/resume" class="nav-link">Resume</router-link>
        <a href="#about" rel="noopener noreferrer" target="_blank" class="nav-link">About Me</a>
        <router-link to="/projects" class="nav-link">Projects</router-link>
        <a href="#blog" rel="noopener noreferrer" target="_blank" class="nav-link">Blog</a>
        <a href='#contact' rel="noopener noreferrer" target="_blank" class='nav-link'>Contact Me</a>
      </div>

      <!-- Mobile Menu Button -->
      <button @click="toggleMenu" class="md:hidden">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path v-if="!isOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
          <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </nav>

    <!-- Mobile Menu -->
    <transition name="fade">
      <div v-if="isOpen" class="md:hidden bg-secondary pb-4">
        <router-link to="/resume" @click="toggleMenu" class="block py-2 px-6 text-gray-700 hover:bg-primary hover:text-secondary transition-colors duration-200">Resume</router-link>
        <a href="#about" rel="noopener noreferrer" target="_blank" @click="toggleMenu" class="block py-2 px-6 text-gray-700 hover:bg-primary hover:text-secondary transition-colors duration-200">About Me</a>
        <router-link to="/projects" @click="toggleMenu" class="block py-2 px-6 text-gray-700 hover:bg-primary hover:text-secondary transition-colors duration-200">Projects</router-link>
        <a href="#blog" rel="noopener noreferrer" target="_blank" @click="toggleMenu" class="block py-2 px-6 text-gray-700 hover:bg-primary hover:text-secondary transition-colors duration-200">Blog</a>
        <a href="#contact"  rel="noopener noreferrer" target="_blank" @click="toggleMenu" class="block py-2 px-6 text-gray-700 hover:bg-primary hover:text-secondary transition-colors duration-200">Contact Me</a>
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
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

h1, h2, h3, h4, h5, h6 {
    font-family: 'Lora', serif;
}

.bg-primary { background-color: #6F4E37; } 
.text-primary { color: #6F4E37; }
.border-primary { border-color: #6F4E37; }
.bg-secondary { background-color: #FDFBF7; }
.text-secondary { color: #FDFBF7; }
.accent-color { color: #A0522D; } 


.nav-link {
  position: relative; 
  transition: color 0.3s ease-in-out;
}

.nav-link::after {
  content: '';
  position: absolute;
  width: 100%;
  transform: scaleX(0); 
  height: 2px;
  bottom: -4px; 
  left: 0;
  background-color: #6F4E37; 
  transform-origin: bottom right;
  transition: transform 0.3s ease-in-out;
}

.nav-link:hover {
  color: #6F4E37; 
}

.nav-link:hover::after {
  transform: scaleX(1); 
  transform-origin: bottom left;
}
</style>
