<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import type { Event } from '@/types'
import { ref, onMounted, computed, watch } from 'vue'
import EventService from '@/services/EventService'

const events = ref<Event[] | null>(null)
const totalEvents = ref<number>(0)

const props = defineProps({
  page: {
    type: Number,
    required: true
  },
  perPage: {
    type: Number,
    required: true
  }
})

const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / props.perPage)
  return props.page < totalPages
})

const fetchEvents = () => {
  EventService.getEvents(props.perPage, props.page)
    .then((response) => {
      events.value = response.data
      totalEvents.value = response.headers['x-total-count']
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
}

onMounted(fetchEvents)

watch(
  () => [props.page, props.perPage],
  fetchEvents
)
</script>

<template>
  <h1>Events For Good</h1>
  <div class="flex flex-col items-center">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>

  <div class="flex w-[290px]">
    <RouterLink
      id="page-prev"
      class="flex-1 no-underline text-gray-700 text-left"
      :to="{ name: 'event-list-view', query: { page: page - 1, perPage: perPage } }"
      rel="prev"
      v-if="page != 1"
      >&#60; Prev Page</RouterLink
    >

    <RouterLink
      id="page-next"
      class="flex-1 no-underline text-gray-700 text-right"
      :to="{ name: 'event-list-view', query: { page: page + 1, perPage: perPage } }"
      rel="next"
      v-if="hasNextPage"
      >Next Page &#62;</RouterLink
    >
  </div>
</template>
