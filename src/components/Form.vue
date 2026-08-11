<script setup>
import { ref } from 'vue'

const form = ref({
  name: '',
  email: '',
  message: ''
})

const submitted = ref(false)

const handleSubmit = () => {
  if (form.value.name && form.value.email && form.value.message) {
    submitted.value = true
    console.log('Form submitted:', form.value)
    setTimeout(() => {
      form.value = { name: '', email: '', message: '' }
      submitted.value = false
    }, 2000)
  }
}
</script>

<template>
  <div class="form-container">
    <header class="form-header">
      <div>
        <p class="form-subtitle">Panel de Gestión</p>
        <h2>Formulario de Contacto</h2>
      </div>
      <span class="form-tag">Nuevo</span>
    </header>

    <div v-if="submitted" class="success-message">
      ¡Formulario enviado correctamente!
    </div>

    <form @submit.prevent="handleSubmit" class="form-card">
      <div class="form-grid">
        <div class="form-group">
          <label for="name">Nombre</label>
          <input
            id="name"
            v-model="form.name"
            type="text"
            placeholder="Ingrese su nombre"
            required
          />
        </div>

        <div class="form-group">
          <label for="email">Email</label>
          <input
            id="email"
            v-model="form.email"
            type="email"
            placeholder="correo@ejemplo.com"
            required
          />
        </div>
      </div>

      <div class="form-group">
        <label for="message">Mensaje</label>
        <textarea
          id="message"
          v-model="form.message"
          placeholder="Cuéntanos tu consulta..."
          rows="5"
          required
        ></textarea>
      </div>

      <div class="actions-row">
        <button type="submit" class="submit-btn">Enviar mensaje</button>
      </div>
    </form>
  </div>
</template>


