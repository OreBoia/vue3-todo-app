<template>
  <div>
    <h1>Componente Padre</h1>

    <!-- Passiamo una prop -->
    <ChildComponent
      :message="parentMessage"
      @notify="handleNotify"
    />

    <p>Risposta del figlio: {{ childResponse }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ChildComponent from './ChildSimpleExample.vue'

/* Stato del padre */
const parentMessage = 'Ciao figlio, come stai?'
const childResponse = ref('')

/* Gestore evento emesso dal figlio */
function handleNotify(payload: string) {
  childResponse.value = payload
}
</script>
