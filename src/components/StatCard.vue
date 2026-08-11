<script setup>
defineProps({
  label: {
    type: String,
    required: true
  },
  value: {
    type: Number,
    required: true
  },
  icon: {
    type: String,
    default: '📊'
  },
  color: {
    type: String,
    default: '#3498db'
  }
})
</script>

<template>
  <div class="stat-card" :style="{ borderTopColor: color }">
    <div class="icon">{{ icon }}</div>
    <div class="content">
      <p class="value">{{ value }}</p>
      <p class="label">{{ label }}</p>
    </div>
    <button class="info-btn">Más info →</button>
  </div>
</template>

<style scoped>
.stat-card {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95) 0%, rgba(250, 250, 250, 0.95) 100%);
  border-radius: 8px;
  border-top: 4px solid;
  padding: 1rem 1.2rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  gap: 1rem;
  transition: transform 0.3s, box-shadow 0.3s;
  cursor: pointer;
}

.stat-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
}

.icon {
  font-size: 2rem;
  flex-shrink: 0;
}

.content {
  flex: 1;
}

.value {
  margin: 0;
  font-size: 1.5rem;
  font-weight: 700;
  color: #2c3e50;
}

.label {
  margin: 0.15rem 0 0 0;
  font-size: 0.85rem;
  color: #7f8c8d;
  font-weight: 500;
}

.info-btn {
  background-color: transparent;
  border: none;
  color: #3498db;
  cursor: pointer;
  font-size: 0.8rem;
  font-weight: 600;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  transition: background-color 0.3s;
  white-space: nowrap;
}

.info-btn:hover {
  background-color: rgba(52, 152, 219, 0.1);
  color: #2980b9;
}
</style>
