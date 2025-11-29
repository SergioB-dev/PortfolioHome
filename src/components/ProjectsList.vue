<script setup lang="ts">
import { onMounted, ref } from 'vue'
import type { Project } from '@/models/Project'
import ProjectCard from './ProjectCard.vue'

const projects = ref<Project[]>([])
const isLoading = ref(false)
const error = ref<string | null>(null)

// Use environment variable for API base URL
const API_BASE_URL =
  import.meta.env.VITE_API_BASE_URL || 'https://acbackendswift-90223035273.us-east4.run.app'
const API_URL = import.meta.env.DEV
  ? '/api/projects' // Use proxy in development
  : `${API_BASE_URL}/projects` // Use full URL in production

async function fetchProjects() {
  error.value = null
  isLoading.value = true
  try {
    const response = await fetch(API_URL, {
      method: 'GET',
      mode: 'cors',
      headers: {
        'Content-Type': 'application/json',
      },
    })
    if (!response.ok) {
      throw new Error(`Failed with status ${response.status}`)
    }
    const data = await response.json()
    projects.value = Array.isArray(data) ? data : [data]
  } catch (err) {
    if (err instanceof TypeError && err.message.includes('fetch')) {
      error.value =
        'CORS error: Backend must allow requests from this origin. Check backend CORS configuration.'
    } else {
      error.value = err instanceof Error ? err.message : 'Unexpected error'
    }
  } finally {
    isLoading.value = false
  }
}

onMounted(fetchProjects)
</script>

<template>
  <section class="projects">
    <p v-if="error" class="status error">⚠️ {{ error }}</p>
    <p v-else-if="!projects.length" class="status">No projects to show.</p>

    <ul v-else>
      <li v-for="project in projects" :key="project.id">
        <ProjectCard :project="project" />
      </li>
    </ul>
  </section>
</template>

<style scoped>
button {
  padding: 0.4rem 1.2rem;
  border-radius: 999px;
  border: 1px solid var(--color-border);
  background: var(--color-background-mute);
  cursor: pointer;
  transition: opacity 0.2s;
}

button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.status {
  font-style: italic;
  color: var(--color-text);
}

.status.error {
  color: #e63946;
}

ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

/* li {
  border: 1px solid var(--color-border);
  border-radius: 8px;
  padding: 0.75rem;
  background: var(--color-background-mute);
} */
</style>
