<template>
  <div class="not-found">
    <h1>404 - Pagina non trovata</h1>
    <p>La pagina che stai cercando non esiste.</p>
    <router-link to="/">Torna alla Home</router-link>
  </div>
</template>

<script setup lang="ts">

</script>

<style scoped>
.not-found {
  text-align: center;
  margin-top: 100px;
}
.not-found h1 {
  font-size: 3em;
  color: #e74c3c;
}
.not-found p {
  margin: 20px 0;
  font-size: 1.2em;
}
</style>
