<script setup>
import { onMounted, ref } from 'vue'
import EventService from '@/services/EventService'

const props = defineProps({
  id: {
    required: true,
  },
})

const event = ref(null)

onMounted(() => {
  EventService.getEvent(props.id)
    .then((response) => {
      event.value = response.data
    })
    .catch((error) => {
      console.error('Error fetching events:', error)
    })
})
</script>

<template>
  <div v-if="event">
    <h2>{{ event.title }}</h2>
    <span>@{{ event.time }} on {{ event.date }}</span>
  </div>
</template>

<style scoped></style>
