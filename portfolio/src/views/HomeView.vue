<script setup>
import NavBar from '../components/NavBar.vue';
import TheHeader from '../components/TheHeader.vue';
import AboutMe from '../components/AboutMe.vue';
import TheProjects from '../components/TheProjects.vue';
import BlogSection from '../components/BlogSection.vue';
import MyResume from '../components/MyResume.vue';
import ContactMe from '../components/ContactMe.vue';
import TheFooter from '../components/TheFooter.vue';
</script>

<template>
  <header>
    <NavBar />
  </header>
  <main>
    <TheHeader />
    <AboutMe />
    <TheProjects />
    <BlogSection />
    <MyResume />
    <ContactMe />
  </main>
  <footer>
    <TheFooter />
  </footer>
</template>