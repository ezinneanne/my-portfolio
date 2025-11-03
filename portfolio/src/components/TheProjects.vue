<template>
  <!-- Projects Section -->
  <section id="projects" class="py-20 md:py-28">
    <div class="container mx-auto px-6">
      <h2 class="text-3xl font-bold text-primary text-center mb-12">Projects</h2>
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div
          v-for="project in projects"
          :key="project.title"
          class="bg-white rounded-lg shadow-lg overflow-hidden transform hover:-translate-y-2 transition-transform duration-300"
        >
        
          <img
            :src="project.image"
            :alt="project.title"
            class="w-full h-48 object-cover"
          />
          <div class="p-6">
            <h3 class="text-xl font-bold text-primary mb-2">
              {{ project.title }}
            </h3>
            <p class="text-gray-600 text-sm mb-4">{{ project.description }}</p>
            <div class="flex flex-wrap gap-2 mb-4">
              <span
                v-for="tag in project.tags"
                :key="tag"
                class="bg-gray-200 text-gray-700 text-xs font-semibold px-2 py-1 rounded-full"
              >
                {{ tag }}
              </span>
            </div>
            <a
              :href="project.link"
              target="_blank"
              class="text-primary font-semibold hover:underline"
              >View Project &rarr;</a
            >
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";
import pharmaImg from "../assets/pharma-compliance-agent.png";


// reactive state using Composition API
const projects = ref([
  {
    title: "Multi-agent Pharma Compliance System",
    description:
      "An AI agent that validates pharma batch data, then automates compliance reports or corrective actions.",
    image: pharmaImg,
    tags: ["n8n", "Google Drive API", "Slack API", "Jira API", "Twilio API"],
    video: "#",
    documentation: "#"
  },
  {
    title: "Sentiment Analysis Chatbot",
    description:
      "An NLP model trained to analyze user input sentiment in real-time, integrated into a customer support chatbot.",
    image: "https://placehold.co/600x400/A0522D/FDFBF7?text=Project+2",
    tags: ["Python", "TensorFlow", "NLP", "Flask"],
    link: "#",
  },
  {
    title: "Automated Code Snippet Validator",
    description:
      "A tool that automatically tests code snippets in markdown files to ensure they are correct and up-to-date.",
    image: "https://placehold.co/600x400/4A3F35/FDFBF7?text=Project+3",
    tags: ["Node.js", "Automation", "Testing", "DevOps"],
    link: "#",
  },
]);
</script>

<style>
/* Add any extra styles here */
</style>
