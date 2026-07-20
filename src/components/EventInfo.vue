<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="event-info">
    <span class="category">{{ event.category }}</span>
    <span class="organizer">{{ event.organizer }}</span>
  </div>
</template>

<style scoped>
.event-info {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
.category {
  font-size: 14px;
  text-align: right;
}
.organizer {
  font-size: 14px;
  text-align: right;
}
</style>