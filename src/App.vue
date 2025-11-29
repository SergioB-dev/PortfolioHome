<script setup lang="ts">
import { RouterLink } from 'vue-router'
import ProjectsList from '@/components/ProjectsList.vue'
import { Analytics } from '@vercel/analytics/vue'
</script>

<template>
  <Analytics />
  <div class="main-container">
    <header>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/projects">Projects</RouterLink>
      </nav>
    </header>

    <div class="top-cards">
      <img src="@/assets/selfie.jpg" class="selfie" />
      <!-- <RouterView /> -->
      <ProjectsList />
    </div>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  width: 100%;
  max-height: 100vh;
}

nav {
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
  top: 0;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

.projects {
  margin-top: 5rem;
}

.selfie {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  margin: 2rem auto;
  display: block;
}

nav a {
  /* display: inline-block; */
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}
</style>
