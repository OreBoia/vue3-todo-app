<template>
  <p>{{ user.nome }} - Età: {{ user.eta }}</p>
  <p v-if="isAdmin">Sei un amministratore</p>
</template>

<script setup lang="ts">
interface User {
  nome: string
  eta: number
}

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const props = defineProps<{
  user: User
  isAdmin?: boolean
}>()
</script>
