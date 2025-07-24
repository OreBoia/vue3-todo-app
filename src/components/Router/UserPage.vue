<template>
  <div class="user-page">
    <nav class="breadcrumb">
      <RouterLink to="/users" class="back-link">← Torna alla lista utenti</RouterLink>
    </nav>

    <div v-if="loading" class="loading">
      Caricamento dettagli utente...
    </div>

    <div v-else-if="user" class="user-details">
      <div class="user-header">
        <div class="user-avatar">
          {{ user.name.charAt(0).toUpperCase() }}
        </div>
        <div class="user-title">
          <h1>{{ user.name }}</h1>
          <p class="user-subtitle">ID: {{ user.id }}</p>
        </div>
      </div>

      <div class="user-info">
        <div class="info-card">
          <h3>Informazioni Utente</h3>
          <div class="info-item">
            <strong>Nome:</strong> {{ user.name }}
          </div>
          <div class="info-item">
            <strong>Email:</strong> {{ user.email }}
          </div>
          <div class="info-item">
            <strong>ID:</strong> {{ user.id }}
          </div>
        </div>
      </div>
    </div>

    <div v-else class="error">
      <h2>Utente non trovato</h2>
      <p>L'utente con ID {{ userId }} non esiste.</p>
      <RouterLink to="/users" class="btn btn-primary">Torna alla lista utenti</RouterLink>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import { useRoute } from 'vue-router'

interface User {
  id: number
  name: string
  email: string
}

const route = useRoute()
const user = ref<User | null>(null)
const loading = ref(true)

// Otteniamo l'ID dall'URL
const userId = computed(() => route.params.id as string)

// Dati semplificati per gli utenti
const usersData: Record<string, User> = {
  '1': { id: 1, name: 'Mario Rossi', email: 'mario.rossi@email.com' },
  '2': { id: 2, name: 'Anna Verdi', email: 'anna.verdi@email.com' },
  '3': { id: 3, name: 'Luigi Bianchi', email: 'luigi.bianchi@email.com' }
}

onMounted(() => {
  // Simuliamo caricamento dati
  setTimeout(() => {
    user.value = usersData[userId.value] || null
    loading.value = false
  }, 300)
})
</script>

<style scoped>
.user-page {
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.breadcrumb {
  margin-bottom: 2rem;
}

.back-link {
  color: #3498db;
  text-decoration: none;
  font-weight: 500;
}

.back-link:hover {
  text-decoration: underline;
}

.loading {
  text-align: center;
  padding: 4rem;
  font-size: 1.2rem;
  color: #7f8c8d;
}

.user-header {
  display: flex;
  align-items: center;
  margin-bottom: 3rem;
  padding-bottom: 2rem;
  border-bottom: 2px solid #ecf0f1;
}

.user-avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background: linear-gradient(135deg, #3498db, #2980b9);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  font-weight: bold;
  margin-right: 2rem;
}

.user-title h1 {
  margin: 0 0 0.5rem 0;
  color: #2c3e50;
  font-size: 2.5rem;
}

.user-subtitle {
  margin: 0;
  color: #7f8c8d;
  font-size: 1.1rem;
}

.user-info {
  max-width: 600px;
  margin: 0 auto 2rem auto;
}

.info-card {
  background: #f8f9fa;
  border-radius: 8px;
  padding: 2rem;
  border-left: 4px solid #3498db;
}

.info-card h3 {
  margin: 0 0 1.5rem 0;
  color: #2c3e50;
  font-size: 1.3rem;
}

.info-item {
  margin-bottom: 1rem;
  padding: 0.5rem 0;
  border-bottom: 1px solid #e1e5e9;
}

.info-item:last-child {
  border-bottom: none;
  margin-bottom: 0;
}

.info-item strong {
  color: #2c3e50;
  margin-right: 0.5rem;
}

.error {
  text-align: center;
  padding: 4rem;
}

.error h2 {
  color: #e74c3c;
  margin-bottom: 1rem;
}

.error p {
  color: #7f8c8d;
  margin-bottom: 2rem;
}
</style>
