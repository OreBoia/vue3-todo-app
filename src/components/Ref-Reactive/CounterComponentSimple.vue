<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'

// ref per un valore singolo
const count = ref(0)
function increment() { count.value++ }

// reactive per un oggetto complesso
const stato = reactive({ clicks: 0, lastClick: '' })

function tracciaClick() {
  stato.clicks++
  stato.lastClick = new Date().toLocaleTimeString()
}

onMounted(() => console.log('Componente montato'))
</script>
<template>
  <button @click="increment">Hai cliccato {{ count }} volte</button>
  <button @click="tracciaClick">Traccia Click</button>
  <p>Clicks totali: {{ stato.clicks }} - Ultimo click: {{ stato.lastClick }}</p>
</template>
