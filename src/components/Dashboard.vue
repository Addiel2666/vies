<script setup>
import { computed, ref } from 'vue'

const searchQuery = ref('')

const tableData = ref([
  { section: 'EGICO', meta: 290, promoted: 1 },
  { section: 'EGICO', meta: 420, promoted: 1 },
  { section: 'Sección 130', meta: 0, promoted: 1 },
  { section: 'Sección 131', meta: 360, promoted: 1 },
  { section: 'EGICO', meta: 290, promoted: 1 },
  { section: 'Sección 140', meta: 500, promoted: 2 }
])

const filteredData = computed(() => {
  if (!searchQuery.value) return tableData.value
  return tableData.value.filter(item =>
    item.section.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})
</script>

<template>
  <div class="dashboard">


    <!-- Search and Table -->
    <div class="content-section">
      <div class="search-box">
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Buscar por sección..."
          class="search-input"
        />
      </div>

      <table class="data-table">
        <thead>
          <tr>
            <th>Sección</th>
            <th>Meta</th>
            <th>Promovidos</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in filteredData" :key="index">
            <td>{{ item.section }}</td>
            <td>{{ item.meta }}</td>
            <td>{{ item.promoted }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

