<template>
  <div>
    <span :class="{done: todo.completed}">{{ todo.title }}</span>
    <button @click="emit('completed', todo.id)">Completa</button>
    <button @click="emit('edit', { id: todo.id, nuovoTitolo: 'Modificato' })">Modifica</button>
    <button @click="emit('delete', todo.id)">Elimina</button>
  </div>
</template>

<script setup lang="ts">
// eslint-disable-next-line @typescript-eslint/no-unused-vars
  const props = defineProps<{
    todo: {
      id: number;
      title: string;
      completed: boolean
    }
  }>()

  const emit = defineEmits<{
    (e: 'completed', id: number): void
    (e: 'edit', payload: { id: number; nuovoTitolo: string }): void
    (e: 'delete', id: number): void
  }>()
</script>
