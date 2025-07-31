<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventMeta from '@/components/EventMeta.vue'
import type { Event } from '@/types'
import { ref, onMounted, computed, watchEffect } from 'vue'
import EventService from '@/services/EventService'

const events = ref<Event[] | null>(null)
const totalEvents = ref(0)
const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / 3) // 3 = perPage
  return page.value < totalPages
})
const props = defineProps({
  page: {
    type: Number,
    required: true,
  },
  perPage: {
    type: Number,
    required: true,
  },
})
const page = computed(() => props.page)
const perPage = computed(() => props.perPage)

onMounted(() => {
  watchEffect(() => {
    EventService.getEvents(perPage.value, page.value)
      .then((response) => {
        events.value = response.data
        totalEvents.value = Number(response.headers['x-total-count'])
      })
      .catch((error) => {
        console.error('There was an error!', error)
      })
  })
})
</script>

<template>
  <h1>Events For Good</h1>

  <div class="events">
    <div v-for="event in events" :key="event.id">
      <EventCard :event="event" />
      <EventMeta :event="event" />
    </div>

    <div class="pagination">
      <RouterLink
        id="page-prev"
        :to="{ name: 'event-list-view', query: { page: page - 1, perPage: perPage} }"
        rel="prev"
        v-if="page !== 1"
      >
        &#60; Prev Page
      </RouterLink>

      <RouterLink
        id="page-next"
        :to="{ name: 'event-list-view', query: { page: page + 1, perPage: perPage } }"
        rel="next"
        v-if="hasNextPage"
      >
        Next Page &#62;
      </RouterLink>
    </div>
    <div>
      <p>Select items per page:</p>
      <RouterLink :to="{ name: 'event-list-view', query: { page: page, perPage: 2 } }">2</RouterLink> |
      <RouterLink :to="{ name: 'event-list-view', query: { page: page, perPage: 3 } }">3</RouterLink> |
      <RouterLink :to="{ name: 'event-list-view', query: { page: page, perPage: 4 } }">4</RouterLink>
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  width: 290px;
}

.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
</style>
