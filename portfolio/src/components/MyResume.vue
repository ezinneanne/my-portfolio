<template>
  <section id="resume" class="py-20 md:py-28">
    <div class="container mx-auto px-6 text-center">
      <h2 class="text-3xl font-bold text-primary mb-4">My Resume</h2>
      <p class="text-gray-600 mb-8 max-w-2xl mx-auto">
        Here you can find a detailed overview of my professional experience,
        skills, and educational background.
      </p>
      <button
        @click="showResumeModal = true"
        class="bg-primary text-secondary font-bold py-3 px-8 rounded-lg shadow-lg hover:bg-opacity-90 transition-transform transform hover:scale-105"
      >
        View Resume
      </button>
    </div>
  </section>

  <BaseModal v-model="showResumeModal">
    <template #header>
      <h3 class="text-xl font-bold text-primary">My Resume</h3>
    </template>

    <div class="space-y-4">
      <p class="text-gray-600">
        You can view my resume below or download it directly.
      </p>
      <div class="border border-gray-200 rounded-lg overflow-hidden">
        <iframe
          src="/AutoResume.pdf"
          class="w-full"
          height="500"
          title="Ezinne Anne Emilia's Resume"
        ></iframe>
      </div>
      <div class="text-center pt-4">
        <a
          href="/AutoResume.pdf"
          download
          class="bg-primary text-secondary font-bold py-2 px-6 rounded-lg shadow-lg hover:bg-opacity-90 transition-transform transform hover:scale-105"
        >
          Download CV (PDF)
        </a>
      </div>
    </div>
  </BaseModal>
</template>

<script setup>
import { ref } from 'vue'
// Import the modal
import BaseModal from './BaseModal.vue'

const showResumeModal = ref(false)
</script>