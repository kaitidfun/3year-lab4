<script setup lang="ts">
import { toRefs } from 'vue'
import { useRouter } from 'vue-router'
import { type Event } from '@/types'

const props = defineProps<{
  event: Event
  id: string
}>()

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const { event } = toRefs(props)
const router = useRouter()

const register = () => {
  // ✅ ตรงนี้สมมติว่า register สำเร็จ
  // จากนั้น redirect กลับไปยังหน้า event detail
  router.push({
    name: 'event-detail-view'
  })
}
</script>

<template>
  <p>Register event here</p>
  <button @click="register">Register</button>
</template>
