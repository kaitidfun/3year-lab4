<template>
  <h1 style="text-align: center; font-size: 2rem; font-weight: bold;">Students</h1>
  <div class="students">
    <StudentCard v-for="student in students" :key="student.id" :student="student" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import StudentService from '@/services/StudentService'
import StudentCard from '@/components/StudentCard.vue'
import type { Student } from '@/types'

const students = ref<Student[]>([])

onMounted(() => {
  StudentService.getStudents().then((response) => {
    students.value = response.data
  })
})
</script>

<style scoped>
.students {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
