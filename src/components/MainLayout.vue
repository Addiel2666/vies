<script setup>
import { ref } from 'vue'
import Sidebar from './Sidebar.vue'
import DashboardSummary from './DashboardSummary.vue'
import Dashboard from './Dashboard.vue'
import Form from './Form.vue'
import Usuarios from './Usuarios.vue'

const activeMenu = ref('dashboard')

const handleMenuSelect = (menuId) => {
  activeMenu.value = menuId
}
</script>

<template>
  <div class="main-layout">
    <Sidebar @menu-select="handleMenuSelect" />
    
    <div class="main-content">
      <DashboardSummary />

      <!-- Dashboard view -->
      <Dashboard v-show="activeMenu === 'dashboard'" />
      
      <!-- Form view (Contacto) -->
      <Form v-show="activeMenu === 'contacto'" />

      <Usuarios v-show="activeMenu === 'usuarios'" />

      <!-- Placeholder for other sections -->
      <div v-if="activeMenu !== 'dashboard' && activeMenu !== 'contacto' && activeMenu !== 'usuarios'" class="placeholder">
        <h2>{{ activeMenu }}</h2>
        <p>Sección en desarrollo...</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main-layout {
  display: flex;
  height: 100%;
  min-height: 100vh;
  width: 100%;
  background-color: #ecf0f1;
  margin: 0;
  padding: 0;
  overflow: hidden;
  gap: 0;
}

.main-content {
  flex: 1;
  overflow: hidden;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
}

.content {
  flex: 1; /* Ocupa todo el espacio restante horizontalmente */
  width: 100%;
}

.placeholder {
  padding: 2rem;
  text-align: center;
  color: #7f8c8d;
}

.placeholder h2 {
  text-transform: capitalize;
  color: #2c3e50;
}
</style>
