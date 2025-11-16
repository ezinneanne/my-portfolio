<template>
  <section id="contact" class="bg-white py-20 md:py-28">
    <div class="container mx-auto px-6 max-w-3xl text-center">
      <h2 class="text-3xl font-bold text-primary mb-4">Contact Me</h2>
      <p class="text-gray-600 mb-8">
        I'm always open to discussing new projects, creative ideas, or
        opportunities. Feel free to reach out or book a time to chat.
      </p>

      <div
        class="flex flex-col md:flex-row justify-center items-center gap-6 mb-12"
      >
        <a
          href="https://calendar.app.google/CmWMFSEoBMfwdQSt7"
          target="_blank"
          rel="noopener noreferrer"
          class="bg-primary text-secondary font-bold py-3 px-6 rounded-lg shadow-lg hover:bg-opacity-90 transition-transform transform hover:scale-105"
        >
          Book an Appointment
        </a>
      </div>

      <p class="text-gray-600 mb-8">...or send me a message directly:</p>

      <ContactForm />
    </div>
  </section>
</template>

<script setup>
// Import the form component
import ContactForm from './ContactForm.vue'
</script>

<style>
/* No styles needed here */
</style>