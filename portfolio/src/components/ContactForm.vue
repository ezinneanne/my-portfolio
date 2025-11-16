<template>
  <div class="max-w-xl mx-auto">
    <div
      v-if="isSubmitted"
      class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded-lg"
    >
      <strong class="font-bold">Thank you!</strong>
      <p>Your message has been sent successfully. I'll get back to you soon.</p>
    </div>

    <form v-else @submit.prevent="handleSubmit" class="space-y-6">
      <div>
        <label for="name" class="block text-sm font-bold text-gray-700 mb-1"
          >Your Name</label
        >
        <input
          v-model="formData.name"
          type="text"
          name="name"
          id="name"
          required
          class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-primary focus:border-primary"
        />
      </div>

      <div>
        <label for="email" class="block text-sm font-bold text-gray-700 mb-1"
          >Your Email</label
        >
        <input
          v-model="formData.email"
          type="email"
          name="email"
          id="email"
          required
          class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-primary focus:border-primary"
        />
      </div>

      <div>
        <label for="message" class="block text-sm font-bold text-gray-700 mb-1"
          >Message</label
        >
        <textarea
          v-model="formData.message"
          name="message"
          id="message"
          rows="5"
          required
          class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-primary focus:border-primary"
        ></textarea>
      </div>

      <div v-if="error" class="text-red-600">
        <p>Sorry, something went wrong. Please try again.</p>
      </div>

      <div>
        <button
          type="submit"
          :disabled="isLoading"
          class="w-full bg-primary text-secondary font-bold py-3 px-6 rounded-lg shadow-lg hover:bg-opacity-90 transition-transform transform hover:scale-105 disabled:opacity-50 disabled:cursor-not-allowed"
        >
          {{ isLoading ? 'Sending...' : 'Send Message' }}
        </button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Form state
const formData = ref({
  name: '',
  email: '',
  message: '',
})
const isLoading = ref(false)
const isSubmitted = ref(false)
const error = ref(null)


const formspreeEndpoint = 'https://formspree.io/f/meovlwoj'

const handleSubmit = async () => {
  isLoading.value = true
  error.value = null

  try {
    const response = await fetch(formspreeEndpoint, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Accept: 'application/json',
      },
      body: JSON.stringify(formData.value),
    })

    if (response.ok) {
      isSubmitted.value = true
      // Clear form (optional)
      formData.value = { name: '', email: '', message: '' }
    } else {
      throw new Error('Form submission failed')
    }
  } catch (e) {
    error.value = e.message
  } finally {
    isLoading.value = false
  }
}
</script>