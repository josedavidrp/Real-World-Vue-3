<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService.js'

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
      console.log(error)
    })
})
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <nav>
      <RouterLink :to="{ name: 'EventDetails' }">Detalles</RouterLink>
      |
      <RouterLink :to="{ name: 'EventRegister' }">Apuntarse</RouterLink>
      |
      <RouterLink :to="{ name: 'EventEdit' }">Editar</RouterLink>
    </nav>
    <RouterView :event="event" />
  </div>
</template>
