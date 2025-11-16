<template>
  <section id="projects" class="py-20 md:py-28">
    <div class="container mx-auto px-6">
      <h2 class="text-3xl font-bold text-primary text-center mb-12">Projects</h2>
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div
          v-for="project in projects"
          :key="project.title"
          class="bg-white rounded-lg shadow-lg overflow-hidden flex flex-col"
        >
          <img
            :src="project.image"
            :alt="project.title"
            class="w-full h-48 object-cover"
          />
          <div class="p-6 flex flex-col flex-grow">
            <h3 class="text-xl font-bold text-primary mb-2">
              {{ project.title }}
            </h3>
            <p class="text-gray-600 text-sm mb-4">{{ project.description }}</p>
            
            <div class="flex flex-wrap gap-2 mb-4">
  <span
    v-for="tag in project.tags"
    :key="tag"
    class="project-tag" >
    {{ tag }}
  </span>
</div>
            <div class="mt-auto">
              <button
                @click="openProjectModal(project)"
                class="text-primary font-semibold hover:underline"
              >
                View Details &rarr;
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Only render the modal when a project is selected.
       Putting v-if on the component avoids the compiler issues
       that happen when wrapping slot templates with v-if. -->
  <BaseModal v-model="showProjectModal" v-if="selectedProject">
    <template #header>
      <h3 class="text-xl font-bold text-primary">
        {{ selectedProject.title }}
      </h3>
    </template>

    <div class="space-y-6">
      <div class="documentation">
        <h4 class="text-lg font-bold text-gray-800 mb-2">Project Documentation</h4>
        <div class="text-gray-600 leading-relaxed prose" v-html="renderMarkdown(selectedProject.documentation)">
        </div>
      </div>

      <div v-if="selectedProject.youtubeId" class="video-demo">
        <h4 class="text-lg font-bold text-gray-800 mb-2">Video Demo</h4>
        <div class="relative w-full aspect-video overflow-visible">
          <iframe
            :src="`https://www.youtube.com/embed/${selectedProject.youtubeId}`"
            :title="`${selectedProject.title} Video Demo`"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
            class="absolute top-0 left-0 w-full h-full rounded-lg"
          ></iframe>
        </div>
      </div>
    </div>

    <!-- Optional footer slot: a close button (BaseModal uses default slot for body,
         and header slot for header; if your BaseModal supports a footer slot,
         you can add it here. Otherwise the button will be part of the body.) -->
    <template #footer>
      <div class="p-4 border-t border-gray-100 text-right">
        <button
          @click="closeProjectModal"
          class="px-4 py-2 bg-primary text-white rounded-lg"
        >
          Close
        </button>
      </div>
    </template>
  </BaseModal>
</template>

<script setup>
import { ref } from 'vue'
import pharmaImg from '../assets/pharma-compliance-agent.png'
import voiceImg from '../assets/request-return-workflow.png'
import dataImg from '../assets/dataimg.png'
// Import the modal
import BaseModal from './BaseModal.vue'

import { marked } from "marked"

const renderMarkdown = (text) => {
  return marked(text)
}


// Modal state
const showProjectModal = ref(false)
const selectedProject = ref(null)

// Function to open the modal and set the selected project
const openProjectModal = (project) => {
  selectedProject.value = project
  showProjectModal.value = true
}

const closeProjectModal = () => {
  showProjectModal.value = false
  // optional: clear selectedProject after modal close to fully unmount modal content
  // small timeout to allow hide animations to play before clearing (if needed)
  setTimeout(() => {
    selectedProject.value = null
  }, 200)
}

// --- UPDATED PROJECT DATA ---
// I've added 'documentation' and 'youtubeId' fields.
const projects = ref([
  {
    title: 'Multi-agent Pharma Compliance System',
    description:
      'An AI agent that validates pharma batch data, then automates compliance reports or corrective actions.',
    image: pharmaImg,
    tags: ['n8n', 'Google Drive API', 'Slack API', 'Jira API', 'Twilio API'],
    // --- NEW DATA ---
    documentation: `
This system was built to solve the high-risk, time-consuming manual compliance checks in pharmaceutical manufacturing.

## **Core Problem**
Manual validation of batch records is slow and prone to human error, leading to potential compliance failures and costly delays.

### **Solution**
I designed a multi-agent automation using n8n:
1.  **Validator Agent:** An n8n workflow listens for new batch record uploads to a specific Google Drive folder. It uses the Google Drive API to fetch the file and a custom function node to parse the data (e.g., CSV or XML). It validates data against a set of predefined compliance rules (e.g., "Is temperature within 20-25°C?", "Is operator signature present?").

2.  **Reporting Agent:** If all checks pass, this agent is triggered. It generates a summary report and automatically creates a "Passed" ticket in Jira using the Jira API, attaching the summary.

3.  **Alerting Agent:** If any check fails, this agent takes over. It sends an immediate, detailed alert to the quality assurance team's Slack channel (via Slack API) and sends an SMS to the shift supervisor for critical failures (via Twilio API).

This automation reduced manual check time by 95% and eliminated validation-related errors.
`,
    youtubeId: 'prhDj8f-_hg',
    link: '#',
  },
  {
  title: 'A Voice Agent For An eCommerce Store',
  description:
    'A voice agent that handles calls for tracking orders, requesting a return, checking product availability, and checking loyalty rewards.',
  image: voiceImg,
  tags: ['VAPI', 'n8n', 'Gmail'],
  documentation: `
The goal of this project was to build a fully automated **voice agent** that handles customer support calls for an e-commerce store. The agent allows customers to check their order status, request a return, confirm product availability, and check loyalty reward points — all without needing a human support representative.

## **Core Problem**
The store was receiving a high volume of repetitive support calls such as:
- “Where is my order?”
- “Do you have this item in stock?”
- “How do I return a product?”
- “What are my loyalty points?”

Human agents were becoming overwhelmed, resulting in long wait times and inconsistent service quality.

## **Solution**
I designed and deployed a scalable voice agent using **VAPI + n8n + Google Sheets + Gmail**.

### **1. Voice Interaction Layer (VAPI)**
- The agent listens to the customer’s request in real time.
- It identifies the intent: *order tracking*, *product availability*, *return request*, or *loyalty rewards*.
- VAPI forwards structured user data (intent + extracted parameters like order ID or product name) to a webhook URL.

### **2. Automation Workflow (n8n)**
n8n receives the payload from VAPI and processes the request through various branches:

#### **Order Tracking**
- n8n searches a Google Sheet containing customer orders.
- Matches order ID or phone number.
- Returns the order status such as *Processing*, *Shipped*, *Out for Delivery*, or *Delivered*.
- Responds back to VAPI with the appropriate voice message.

#### **Product Availability**
- The workflow checks the store’s inventory sheet.
- Looks up the requested product.
- Sends VAPI a response: *In stock*, *Low stock*, or *Out of stock*.

#### **Return Requests**
- n8n generates a return ticket and sends an email to the customer through Gmail.
- The voice agent also confirms that the return request was submitted successfully.

#### **Loyalty Rewards**
- The system retrieves the customer’s reward balance from a database (Google Sheet).
- VAPI responds with:
“You currently have **XX loyalty points**, equivalent to **XX naira**.”

### **3. Callback Handling & Error Recovery**
- If a customer gives incomplete details (e.g., no order ID), the agent asks follow-up questions.
- If data cannot be found, the call gracefully transfers to a human backup number.

## **Outcome**
- Reduced call-handling workload by over **80%**.
- Provided instant, 24/7 automated support.
- Improved customer satisfaction with faster query resolution.
- Enabled the business to scale support without hiring new staff.
`,
  youtubeId: 'D7QqWp_Bakk',
  link: '#',
},
{
  "title": "A Data Cleaning Agent",
  "description": "An automated agent that receives raw data submissions, validates, cleans and delivers a polished dataset to the user.",
  "image": dataImg,
  "tags": ["n8n", "Gmail API", "Gemini API", "Tally Forms"],
  "documentation": `
  This project showcases a fully automated **Data Cleaning Agent** designed to collect, validate, clean, and deliver structured datasets without human involvement. It was built using **n8n**, **Tally Forms**, **Gemini API**, and **Gmail** to automate the entire workflow from data collection to final cleaned output.

  ## **Core Problem**
  Many teams collect data through forms or manual submissions that often contain:
  - Missing fields  
  - Inconsistent formatting  
  - Incorrect values  
  - Duplicate entries  
  - Poorly structured descriptions  

  Cleaning such data manually takes time and often introduces errors.

  ## **Solution**
  I built an automated agent that:
  1. Captures raw data through **Tally Forms**.
  2. Sends the submitted data to **Gemini** for cleaning, validation, and standardization.
  3. Automatically formats the cleaned result into a structured dataset.
  4. Sends the final cleaned data back to the requester via email using the **Gmail API**.
  5. Logs all submissions for transparency and auditing.

  ## **Outcome**
  - Eliminated manual data cleaning for form submissions.
  - Achieved consistent data quality regardless of user input style.
  - Reduced turnaround time from hours to seconds.
  - Enabled real-time automation for form-heavy internal processes.
  - Improved data reliability for downstream analytics and reporting.

  `,
  "youtubeId": 'yKDLalBzAaA',
  "link": "#"
}
  // ... other projects ...
])
</script>

<style scoped>
.video-demo iframe {
  border: 0;
}

/* Backup styles for project tags */
.project-tag {
  display: inline-block;
  background-color: #e5e7eb; /* bg-gray-200 */
  color: #374151; /* text-gray-700 */
  font-size: 0.75rem; /* text-xs */
  font-weight: 600; /* font-semibold */
  padding-left: 0.5rem; /* px-2 */
  padding-right: 0.5rem; /* px-2 */
  padding-top: 0.25rem; /* py-1 */
  padding-bottom: 0.25rem; /* py-1 */
  border-radius: 9999px; /* rounded-full */
}

</style>
