<template>
  <!-- Blog Section -->
  <section id="blog" class="bg-white py-20 md:py-28">
        <div class="container mx-auto px-6">
        <h2 class="text-3xl font-bold text-primary text-center mb-12">From My Blog</h2>
        <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
        <div v-for="post in blogPosts" :key="post.title" class="border border-gray-200 rounded-lg p-6 hover:shadow-xl hover:border-primary transition-all duration-300">
            <p class="text-sm text-gray-500 mb-1">{{ post.date }}</p>
            <h3 class="text-xl font-bold text-primary mb-2">{{ post.title }}</h3>
            <p class="text-gray-600 mb-4">{{ post.excerpt }}</p>
            <a :href="post.link" target="_blank" class="text-primary font-semibold hover:underline">Read More &rarr;</a>
        </div>
        </div>
        <div class="text-center mt-12">
            <a href="#" class="bg-primary text-secondary font-bold py-3 px-6 rounded-lg shadow-lg hover:bg-opacity-90 transition-transform transform hover:scale-105">Visit Blog</a>
        </div>
        </div>
    </section>
</template>

<script>

</script>

<style>

</style>














