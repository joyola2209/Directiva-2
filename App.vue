<template>
  <div class="app-container">
    <header class="app-header">
      <h1>📚 Gestor Escolar de Notas</h1>
      <p>Llevá el control de tus materias de forma fácil y rápida</p>
    </header>
    
    <main>
      <!-- Llamada al componente hijo -->
      <ControlNotas />
    </main>
  </div>
</template>

<script setup>
import ControlNotas from './components/xxxControlNotas.vue';
</script>

<style>
body {
  margin: 0;
  font-family: 'Segoe UI', Roboto, sans-serif;
  background-color: #f7fafc;
  color: #2d3748;
}

.app-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.app-header {
  text-align: center;
  margin-bottom: 3rem;
}

.app-header h1 {
  font-size: 2.5rem;
  color: #2c3e50;
  margin-bottom: 0.5rem;
}

.app-header p {
  color: #718096;
  font-size: 1.1rem;
}
</style>
