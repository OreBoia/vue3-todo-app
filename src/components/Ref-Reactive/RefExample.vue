<script setup lang="ts">
import { ref } from 'vue'

// Variabile primitiva reattiva
const nome = ref('Mario')

// Cambiando .value si triggera il rendering
function cambiaNome() {
  nome.value = nome.value === 'Mario' ? 'Luigi' : 'Mario'
}
</script>

<template>
  <p>Nome attuale: {{ nome }}</p>
  <button @click="cambiaNome">Cambia Nome</button>
</template>
