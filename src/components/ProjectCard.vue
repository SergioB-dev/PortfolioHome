<template>
  <div class="project-card">
    <img :src="props.project.imageURL" alt="Project Image" class="project-image" />
    <h3>{{ props.project.title }}</h3>
    <p>{{ props.project.summary }}</p>
  </div>
</template>

<script setup lang="ts">
import type { Project } from '@/models/Project'
const props = defineProps<{
  project: Project
}>()

// console.log the props
console.log(props.project.imageURL)
</script>

<style scoped>
.project-image {
  width: 35%;
  height: 35%;
  border-radius: 10px;
  display: block;
  margin: 0 auto;
}
</style>
