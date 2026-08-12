<script setup>
import { ref } from 'vue'

const activeMenu = ref('dashboard')

const menuItems = [
  { id: 'dashboard', label: 'Dashboard', icon: '📊' },
  { id: 'reportes', label: 'Reportes', icon: '📋' },
  { id: 'usuarios', label: 'Usuarios', icon: '👥' },
  { id: 'config', label: 'Configuración', icon: '⚙️' },
  { id: 'organizaciones', label: 'Organizaciones', icon: '🏢' },
  { id: 'contacto', label: 'Contacto', icon: '📧' }
]

const emit = defineEmits(['menu-select'])

const handleMenuClick = (menuId) => {
  activeMenu.value = menuId
  emit('menu-select', menuId)
}
</script>

<template>
  <aside class="sidebar">
    <div class="sidebar-header">
      <div class="logo">📊</div>
      <h1>Panel Admin</h1>
    </div>

    <div class="user-info">
      <div class="user-avatar">👤</div>
      <div class="user-details">
        <p class="user-name">Admin Usuario</p>
        <p class="user-role">Administrador</p>
        <button class="logout-btn">Cerrar Sesión</button>
      </div>
    </div>

    <nav class="menu">
      <button
        v-for="item in menuItems"
        :key="item.id"
        class="menu-item"
        :class="{ active: activeMenu === item.id }"
        @click="handleMenuClick(item.id)"
      >
        <span class="menu-icon">{{ item.icon }}</span>
        <span class="menu-label">{{ item.label }}</span>
      </button>
    </nav>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 250px;
  background-color: #2c3e50;
  color: #ecf0f1;
  display: flex;
  flex-direction: column;
  padding: 0;
  box-shadow: 2px 0 10px rgba(0, 0, 0, 0.1);
  overflow-y: visible;
  flex-shrink: 0;
  box-sizing: border-box;
  margin: 0;
}

.sidebar-header {
  padding: 1rem;
  border-bottom: 1px solid #34495e;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 52px;
  height: 52px;
  font-size: 1.8rem;
}

.sidebar-header h1 {
  margin: 0;
  font-size: 1.3rem;
  font-weight: 600;
  line-height: 1.2;
  color: #ffffff;
}

.user-info {
  padding: 1rem;
  border-bottom: 1px solid #34495e;
  display: flex;
  gap: 0.8rem;
}

.user-avatar {
  width: 50px;
  height: 50px;
  background-color: #34495e;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  flex-shrink: 0;
}

.user-details {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.user-name {
  margin: 0;
  font-weight: 600;
  font-size: 0.95rem;
}

.user-role {
  margin: 0.25rem 0 0 0;
  font-size: 0.85rem;
  color: #bdc3c7;
}

.logout-btn {
  margin-top: 0.5rem;
  padding: 0.4rem 0.8rem;
  background-color: #e74c3c;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 0.75rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

.logout-btn:hover {
  background-color: #c0392b;
}

.menu {
  flex: 1;
  display: flex;
  flex-direction: column;
  padding: 1rem 0;
  list-style: none;
  margin: 0;
}

.menu-item {
  background: none;
  border: none;
  color: #ecf0f1;
  padding: 1rem 1.5rem;
  text-align: left;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 1rem;
  transition: all 0.3s;
  font-size: 0.95rem;
}

.menu-item:hover {
  background-color: #34495e;
  padding-left: 2rem;
}

.menu-item.active {
  background-color: #3498db;
  border-left: 4px solid #2980b9;
  padding-left: calc(1.5rem - 4px);
  font-weight: 600;
}

.menu-icon {
  font-size: 1.2rem;
  width: 24px;
  text-align: center;
}

.menu-label {
  flex: 1;
}
</style>
