<script setup>
import StatCard from './StatCard.vue'
import { panelStats } from '../data/panelStats.js'
</script>

<template>
  <div class="dashboard-summary">
    <h2>Panel de Gestión</h2>
    <div class="cards-grid">
      <StatCard
        v-for="stat in panelStats"
        :key="stat.label"
        :label="stat.label"
        :value="stat.value"
        :icon="stat.icon"
        :color="stat.color"
      />
    </div>
  </div>
</template>

<style scoped>
.dashboard-summary {
  width: 100%;
  padding: 1rem 1.5rem 0.75rem;
  box-sizing: border-box;
}

.dashboard-summary h2 {
  margin: 0 0 1rem;
  font-size: 1.4rem;
  color: #1f3d6b;
}

.cards-grid {
  display: flex;
  gap: 1rem;
  justify-content: space-between;
  flex-wrap: wrap;
  width: 100%;
}

.cards-grid > * {
  flex: 1 1 calc(25% - 0.75rem);
  min-width: 220px;
  max-width: calc(25% - 0.75rem);
}

@media (max-width: 980px) {
  .cards-grid > * {
    flex: 1 1 calc(50% - 0.75rem);
    max-width: calc(50% - 0.75rem);
  }
}

@media (max-width: 640px) {
  .cards-grid > * {
    flex: 1 1 100%;
    max-width: 100%;
  }
}
</style>
