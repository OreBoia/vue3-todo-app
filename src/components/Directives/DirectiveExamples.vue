<template>
  <div>
    <h2>Esempi di Direttive Vue</h2>

    <!-- v-if/v-else -->
    <div>
      <p v-if="loggedIn">Benvenuto!</p>
      <p v-else>Effettua il login</p>
      <button @click="toggleLogin">{{ loggedIn ? 'Logout' : 'Login' }}</button>
    </div>

    <!-- v-show -->
    <div>
      <p v-show="showDetails">Dettagli visibili/nascosti con CSS</p>
      <button @click="toggleDetails">{{ showDetails ? 'Nascondi' : 'Mostra' }} dettagli</button>
    </div>

    <!-- v-for -->
    <div>
      <h3>Lista elementi:</h3>
      <ul>
        <li v-for="(item, i) in items" :key="item.id">{{ i + 1 }} - {{ item.name }}</li>
      </ul>
    </div>

    <!-- Binding attributi -->
    <div>
      <img :src="imageUrl" :alt="descrizione" style="max-width: 200px" />
      <br />
      <button :disabled="isLoading">{{ isLoading ? 'Caricamento...' : 'Invia' }}</button>
      <button @click="toggleLoading">Toggle Loading</button>
    </div>

    <!-- v-model -->
    <div>
      <h3>Input con v-model:</h3>
      <div>
        <label>Username:</label>
        <input v-model="username" placeholder="Inserisci il nome" />
        <p>Nome inserito: {{ username }}</p>
      </div>
      <div>
        <label>Commento:</label>
        <textarea v-model="commento" placeholder="Inserisci un commento"></textarea>
        <p>Commento: {{ commento }}</p>
      </div>
    </div>

    <!-- Event handling -->
    <div>
      <button @click="salvaDati">Salva Dati</button>
      <form @submit.prevent="inviaForm">
        <input type="text" v-model="formData" placeholder="Dati del form" />
        <button type="submit">Invia Form</button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Dati reattivi per v-if/v-else
const loggedIn = ref(false)

// Dati reattivi per v-show
const showDetails = ref(false)

// Dati reattivi per v-for
const items = ref([
  { id: 1, name: 'Primo elemento' },
  { id: 2, name: 'Secondo elemento' },
  { id: 3, name: 'Terzo elemento' },
])

// Dati reattivi per attributi binding
const imageUrl = ref('../../assets/logo.png')
const descrizione = ref('Logo di esempio Vue.js')
const isLoading = ref(false)

// Dati reattivi per v-model
const username = ref('')
const commento = ref('')
const formData = ref('')

// Metodi per gestire gli eventi
function toggleLogin() {
  loggedIn.value = !loggedIn.value
}

function toggleDetails() {
  showDetails.value = !showDetails.value
}

function toggleLoading() {
  isLoading.value = !isLoading.value
}

function salvaDati() {
  console.log('Dati salvati:', {
    username: username.value,
    commento: commento.value,
  })
  alert(`Dati salvati!\nUsername: ${username.value}\nCommento: ${commento.value}`)
}

function inviaForm() {
  console.log('Form inviato con:', formData.value)
  alert(`Form inviato con: ${formData.value}`)
  formData.value = '' // Reset del form
}
</script>

<style scoped>
div {
  margin: 20px 0;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

h2,
h3 {
  color: #42b883;
}

input,
textarea {
  padding: 8px;
  margin: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  margin: 5px;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #369870;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

ul {
  list-style-type: decimal;
  padding-left: 20px;
}

li {
  margin: 5px 0;
}
</style>
