<template>
  <!-- Blog Section -->
  <section id="blog" class="bg-white py-20 md:py-28">
    <div class="container mx-auto px-6">
      <h2 class="text-3xl font-bold text-primary text-center mb-12">
        From My Blog
      </h2>

      <!-- Blog Cards Wrapper -->
      <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
        <!-- Loading State -->
        <div v-if="isLoading" class="md:col-span-2 text-center text-gray-500">
          <p>Loading recent articles...</p>
        </div>

        <!-- Error State -->
        <div v-if="error" class="md:col-span-2 text-center text-red-600">
          <p>Sorry, could not fetch articles. Please try again later.</p>
        </div>

        <!-- Blog Posts -->
        <div
          v-if="!isLoading && !error"
          v-for="post in blogPosts"
          :key="post.title"
          class="border border-gray-200 rounded-lg p-6 hover:shadow-xl hover:border-primary transition-all duration-300"
        >
          <p class="text-sm text-gray-500 mb-1">{{ post.date }}</p>
          <h3 class="text-xl font-bold text-primary mb-2">{{ post.title }}</h3>
          <p class="text-gray-600 mb-4">{{ post.excerpt }}</p>
          <a
            :href="post.link"
            target="_blank"
            rel="noopener noreferrer"
            class="text-primary font-semibold hover:underline"
          >
            Read More →
          </a>
        </div>
      </div>

      <!-- CTA -->
      <div class="text-center mt-12">
        <a
          href="https://medium.com/@ezinneanne" rel="noopener noreferrer" target="_blank"
          class="bg-primary text-secondary font-bold py-3 px-6 rounded-lg shadow-lg hover:bg-opacity-90 transition-transform transform hover:scale-105"
        >
          Visit Blog
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Reactive state for posts, loading, and error
const blogPosts = ref([]);
const isLoading = ref(true);
const error = ref(null);

// Helper function to strip HTML from the description
function stripHtml(html) {
  // Use the browser's built-in parser to safely convert HTML to text
  const doc = new DOMParser().parseFromString(html, 'text/html');
  return doc.body.textContent || "";
}

// Helper function to truncate text
function truncate(text, length) {
  if (text.length <= length) {
    return text;
  }
  return text.substring(0, length) + "...";
}

// Fetch posts when the component is mounted
onMounted(async () => {
  // Your Medium username
  const mediumUsername = "ezinneanne";
  // The API URL to convert your RSS feed to JSON
  const rss2jsonApiUrl = `https://api.rss2json.com/v1/api.json?rss_url=https://medium.com/feed/@${mediumUsername}`;

  try {
    const response = await fetch(rss2jsonApiUrl);
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();

    if (data.status === 'ok') {
      // Map the fetched data to match the structure your component expects
      blogPosts.value = data.items.slice(0, 2).map(item => ({
        title: item.title,
        date: new Date(item.pubDate).toLocaleDateString('en-US', {
          year: 'numeric',
          month: 'long',
          day: 'numeric',
        }),
        // Safely strip HTML from the description and truncate it
        excerpt: truncate(stripHtml(item.description), 150),
        link: item.link,
      }));
    } else {
      throw new Error('Failed to fetch RSS feed');
    }
  } catch (e) {
    error.value = e.message;
    console.error("Failed to fetch Medium posts:", e);
  } finally {
    isLoading.value = false;
  }
});
</script>

<style scoped>
/* Add any extra blog styling here if needed */
</style>
