<template>
  <nav class="fixed top-0 left-0 w-full bg-transparent z-50 font-aeonik">
    <div class="max-w-7xl mx-auto px-6 py-4 flex justify-between items-center">
      
      <!-- Left side links -->
      <ul class="flex space-x-8 text-gray-800">
        <li>
          <a href="#resume" class="hover:underline cursor-pointer">Resume</a>
        </li>
        <li>
          <a href="#about" class="hover:underline cursor-pointer">About Me</a>
        </li>
        <li>
          <a href="#projects" class="hover:underline cursor-pointer">Projects</a>
        </li>
        <li>
          <a href="#blog" class="hover:underline cursor-pointer">Blog</a>
        </li>
      </ul>

      <!-- Right side contact link -->
      <a
        href="#contact"
        class="flex items-center space-x-2 text-gray-800 hover:underline cursor-pointer"
      >
        <span>Contact Me</span>
        <!-- Icon (Mail) -->
        <svg xmlns="http://www.w3.org/2000/svg" 
            class="w-5 h-5" 
            fill="none" 
            viewBox="0 0 24 24" 
            stroke="currentColor" 
            stroke-width="2">
           <path stroke-linecap="round" 
              stroke-linejoin="round" 
              d="M3 8l7.89 5.26c.34.23.78.23 1.12 0L20 8m-17 8h18a2 2 0 002-2V6a2 2 0 00-2-2H3a2 2 0 00-2 2v8a2 2 0 002 2z"
            />
        </svg>
      </a>
    </div>
  </nav>
</template>

<script setup>
// No script logic needed for now
</script>

<style>
/* Import Aeonik font */
@import url('https://fonts.cdnfonts.com/css/aeonik');

.font-aeonik {
  font-family: 'Aeonik', sans-serif;
}
</style>
