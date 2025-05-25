<script setup>
import { useRouter } from 'vue-router'
const props = defineProps(['event'])
const router = useRouter()
const register = () => {
  //Si el registro es correcto, volver a los detalles del evento
  router.push({
    name: 'EventDetails',
  })
}
</script>

<template>
  <p>Apúntate al evento aquí</p>
  <button @click="register">¡Apúntame!</button>
</template>
