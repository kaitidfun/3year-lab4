<!-- src/components/StudentCard.vue -->
<template>
  <div class="student-card">
    <img :src="student.image" :alt="student.name" class="student-image" />
    <h2>{{ student.name }} {{ student.surname }}</h2>
    <p>GPA: {{ student.gpa }}</p>
    <p>{{ student.description }}</p>
  </div>
</template>

<script setup lang="ts">
import type { Student } from '@/types'
defineProps<{ student: Student }>()
</script>

<style scoped>
.student-card {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 16px;
  margin-bottom: 16px;
  width: 300px;
  text-align: center;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}
.student-card:hover {
  transform: scale(1.03);
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.15);
}
.student-image {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 12px;
}
</style>
