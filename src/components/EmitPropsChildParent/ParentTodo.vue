<template>
  <TodoItem :todo="sampleTodo" @completed="markCompleted" @edit="editTask" @delete="removeTask" />
</template>

<script setup lang="ts">
  import TodoItem from './TodoItem.vue'
  import { ref } from 'vue'

  // Esempio di todo
  const sampleTodo = ref({
    id: 1,
    title: 'Task di esempio',
    completed: false,
  })

  function markCompleted(id: number) {
    console.log('Completo', id)
    sampleTodo.value.completed = !sampleTodo.value.completed
  }

  function editTask(payload: { id: number; nuovoTitolo: string }) {
    console.log('Edit', payload)
    sampleTodo.value.title = payload.nuovoTitolo
  }

  function removeTask(id: number) {
    console.log('Rimuovo', id)
  }
</script>
