<template>
  <div class="users-list">
    <h2>Lista Utenti</h2>
    <p>Clicca su un utente per vedere il suo profilo:</p>
    <ul class="user-grid">
      <li v-for="user in users" :key="user.id" class="user-card">
        <!-- Link alla pagina utente dinamica -->
        <RouterLink :to="`/users/${user.id}`" class="user-link">
          <div class="user-info">
            <h3>{{ user.name }}</h3>
            <p>{{ user.email }}</p>
            <span class="user-role">{{ user.role }}</span>
          </div>
        </RouterLink>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

interface User {
  id: number
  name: string
  email: string
  role: string
}

const users = ref<User[]>([])

// Simuliamo il caricamento di dati utenti
onMounted(() => {
  // In una app reale, questi dati potrebbero venire da un'API
  users.value = [
    { id: 1, name: 'Mario Rossi', email: 'mario.rossi@email.com', role: 'Developer' },
    { id: 2, name: 'Anna Verdi', email: 'anna.verdi@email.com', role: 'Designer' },
    { id: 3, name: 'Luigi Bianchi', email: 'luigi.bianchi@email.com', role: 'Manager' },
    { id: 4, name: 'Sofia Neri', email: 'sofia.neri@email.com', role: 'Developer' },
    { id: 5, name: 'Marco Gialli', email: 'marco.gialli@email.com', role: 'Tester' }
  ]
})
</script>

<style scoped>
.users-list {
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.users-list h2 {
  color: #2c3e50;
  margin-bottom: 1rem;
}

.user-grid {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.user-card {
  border: 1px solid #e1e5e9;
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.2s, box-shadow 0.2s;
}

.user-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.user-link {
  display: block;
  text-decoration: none;
  color: inherit;
  padding: 1.5rem;
}

.user-info h3 {
  margin: 0 0 0.5rem 0;
  color: #2c3e50;
  font-size: 1.2rem;
}

.user-info p {
  margin: 0 0 0.75rem 0;
  color: #7f8c8d;
  font-size: 0.9rem;
}

.user-role {
  display: inline-block;
  background: #3498db;
  color: white;
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: 500;
}
</style>
