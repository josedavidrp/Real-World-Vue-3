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
    <div id="nav">
      <router-link :to="{ name: 'EventDetails', params: { id } }">Detalles</router-link>
      |
      <router-link :to="{ name: 'EventRegister', params: { id } }">Apuntarse</router-link>
      |
      <router-link :to="{ name: 'EventEdit', params: { id } }">Editar</router-link>
    </div>
    <router-view :event="event" />
  </div>
</template>
