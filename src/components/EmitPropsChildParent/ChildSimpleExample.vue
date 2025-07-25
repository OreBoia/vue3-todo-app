<template>
  <div>
    <!-- Mostriamo la prop ricevuta -->
    <p>Messaggio dal padre: {{ message }}</p>

    <!-- Quando clicchi, il figlio emette un evento al padre -->
    <button @click="notifyParent">Avvisa il padre</button>
  </div>
</template>

<script setup lang="ts">
/*  Definiamo le props che il figlio può ricevere */
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const props = defineProps<{
  message: string
}>()

/*  Definiamo gli eventi che il figlio può emettere */
const emit = defineEmits<{
  (e: 'notify', payload: string): void
}>()

/* Funzione per emettere l'evento */
function notifyParent() {
  emit('notify', 'Ciao dal figlio!')
}
</script>
