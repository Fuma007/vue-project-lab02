<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventInfo from '@/components/EventInfo.vue'
import type { Event } from '@/types'
import { ref } from 'vue'

const events = ref<Event[] | null>(null)
</script>

<template>
  <h1>Events For Good</h1>

  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <EventInfo v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
    .events {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>