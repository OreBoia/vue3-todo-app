<script setup lang="ts">
import { reactive, watch } from 'vue'

// Oggetto reattivo con più campi
const form = reactive({ username: '', email: '', password: '' })

// Funzione di submit
function submitForm() {
  console.log('Dati inviati:', form.username, form.email, form.password)
}

// Watch per reagire ai cambiamenti dell'email
watch(() => form.email, (nuovo, vecchio) => {
  console.log(`Email cambiata da ${vecchio} a ${nuovo}`)
})
</script>

<template>
  <form @submit.prevent="submitForm">
    <input v-model="form.username" placeholder="Username" />
    <input v-model="form.email" placeholder="Email" />
    <input v-model="form.password" type="password" placeholder="Password" />
    <button type="submit">Invia</button>
  </form>

  <p>Preview: {{ form.username }} - {{ form.email }}</p>
</template>
