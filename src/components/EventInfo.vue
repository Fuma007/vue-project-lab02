<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="flex flex-col items-end">
    <span class="text-sm text-right">{{ event.category }}</span>
    <span class="text-sm text-right">{{ event.organizer }}</span>
  </div>
</template>