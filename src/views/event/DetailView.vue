<script setup lang="ts">
import { toRefs, defineProps } from 'vue'
import { type Event } from '@/types'
import { onMounted } from 'vue'
import { useMessageStore } from '@/stores/message'
import { storeToRefs } from 'pinia'

const props = defineProps<{
  event: Event
  id: string
}>()

const { event } = toRefs(props)
const store = useMessageStore()
const { message } = storeToRefs(store)

onMounted(() => {
  if (message.value) {
    setTimeout(() => {
      store.resetMessage()
    }, 3000)
  }
})
</script>

<template>
  <div>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>
