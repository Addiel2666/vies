<script setup>
import { computed, ref } from 'vue'
import StatCard from './StatCard.vue'
import { panelStats } from '../data/panelStats.js'

const stats = panelStats
const searchQuery = ref('')
const mostrarModal = ref(false)

</script>

<template>
  <div class="dashboard">



    <!-- Search and Table -->
    <div class="content-section">
      <h2>Administrar Usuarios</h2>
<div class="container">
    <!-- Botón para abrir el popup -->
    <button class="btn-open" @click="mostrarModal = true">
      Abrir Popup
    </button>

    <!-- Fondo oscuro y ventana emergente -->
    <div v-if="mostrarModal" class="modal-overlay" @click.self="mostrarModal = false">
      <div class="modal-content">
       <p>Message is: {{ message }}</p>
<input v-model="message" placeholder="edit me" />
        
        <!-- Botón para cerrar -->
        <button class="btn-close" @click="mostrarModal = false">
          Cerrar
        </button>
      </div>
    </div>
  </div>
    </div>
  </div>
</template>


