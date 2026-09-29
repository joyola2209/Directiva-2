<template>
  <div class="control-notas">
    <h2>Ingreso de Calificaciones</h2>
    
    <!-- Formulario -->
    <form @submit.prevent="agregarNota" class="formulario">
      <div class="campo">
        <label for="materia">Materia:</label>
        <input id="materia" v-model.trim="nuevaNota.materia" type="text" placeholder="Ej: Matemática" required />
      </div>

      <div class="campo">
        <label for="fecha">Fecha:</label>
        <input id="fecha" v-model="nuevaNota.fecha" type="date" required />
      </div>

      <div class="campo">
        <label for="nota">Nota (1 al 10):</label>
        <input id="nota" v-model.number="nuevaNota.valor" type="number" step="0.1" placeholder="Ej: 8.5" required />
      </div>

      <button type="submit" class="btn-guardar">Guardar Nota</button>
    </form>

    <!-- Mensaje de Error si la nota está mal -->
    <div v-if="errorMensaje" class="alerta-error">
      {{ errorMensaje }}
    </div>

    <!-- Tabla de Notas -->
    <div class="listado-notas">
      <h3>Historial de Notas</h3>
      <p v-if="notas.length === 0" class="sin-datos">No hay notas registradas todavía.</p>
      
      <table v-else class="tabla-notas">
        <thead>
          <tr>
            <th>Materia</th>
            <th>Fecha</th>
            <th>Nota</th>
            <th>Estado</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in notas" :key="index">
            <td>{{ item.materia }}</td>
            <td>{{ item.fecha }}</td>
            <td class="nota-valor">{{ item.valor }}</td>
            <td :class="['estado', item.valor >= 6 ? 'aprobado' : 'desaprobado']">
              {{ item.valor >= 6 ? 'Aprobado' : 'Desaprobado' }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';

const notas = ref([]);
const errorMensaje = ref('');

const nuevaNota = reactive({
  materia: '',
  fecha: '',
  valor: null
});

const agregarNota = () => {
  errorMensaje.value = '';

  // Validación requerida por la consigna (del 1 al 10)
  if (isNaN(nuevaNota.valor) || nuevaNota.valor < 1 || nuevaNota.valor > 10) {
    errorMensaje.value = '¡Error! La nota debe ser un número entre 1 y 10.';
    return;
  }

  // Si pasa la validación, se guarda
  notas.value.push({
    materia: nuevaNota.materia,
    fecha: nuevaNota.fecha,
    valor: nuevaNota.valor
  });

  // Limpiar formulario
  nuevaNota.materia = '';
  nuevaNota.fecha = '';
  nuevaNota.valor = null;
};
</script>

<style scoped>
.control-notas {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}
.formulario {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 2rem;
  align-items: flex-end;
}
.campo {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}
input {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.btn-guardar {
  background-color: #42b883;
  color: white;
  border: none;
  padding: 0.6rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
.alerta-error {
  background-color: #fed7d7;
  color: #c53030;
  padding: 1rem;
  border-left: 5px solid #e53e3e;
  margin-bottom: 1rem;
}
.tabla-notas {
  width: 100%;
  border-collapse: collapse;
}
.tabla-notas th, .tabla-notas td {
  padding: 8px;
  border-bottom: 1px solid #eee;
  text-align: left;
}
.estado {
  font-weight: bold;
  padding: 2px 6px;
  border-radius: 4px;
}
.aprobado {
  background-color: #e6fffa;
  color: green;
}
.desaprobado {
  background-color: #fff5f5;
  color: red;
}
</style>
