<script setup>
import { ref, onMounted, computed } from 'vue'

const selectedFile = ref(null)
const previewUrl = ref(null)
const isUploading = ref(false)

const handleFileUpload = async (event) => {
  const file = event.target.files?.[0]
  if (!file) return

  selectedFile.value = file
  previewUrl.value = URL.createObjectURL(file)

  try {
    const arrayBuffer = await file.arrayBuffer()
    const bytes = Array.from(new Uint8Array(arrayBuffer))

    form.value.photo = bytes
    form.value.photoName = file.name
    form.value.photoType = file.type
  } catch (error) {
    console.error('Error al leer el archivo:', error)
    form.value.photo = null
    form.value.photoName = ''
    form.value.photoType = ''
  }
}

const uploadImage = async () => {
  if (!selectedFile.value) return

  isUploading.value = true

  const formData = new FormData()
  formData.append('photo', selectedFile.value)

  try {
    const response = await fetch('https://tu-api.com/upload', {
      method: 'POST',
      body: formData,
    })

    if (!response.ok) {
      throw new Error('Error en la subida')
    }

    const data = await response.json()
    console.log('Imagen subida con éxito:', data)
    alert('¡Imagen subida correctamente!')
  } catch (error) {
    console.error('Error al subir la imagen:', error)
    alert('Error al subir la imagen.')
  } finally {
    isUploading.value = false
  }
}

const mostrarModal = ref(false)
const form = ref({
  name: '',
  user: '',
  password: '',
  repeatPass: '',
  idPerfil: '',
  photo: null,
  photoName: '',
  photoType: '',
})
const showPassword = ref(false)

const opciones = ref([])
const isLoading = ref(true)
const errorMsg = ref(null)
const mensajeExito = ref('')
const cargando = ref(false)

// Función para consumir la API GET
const apiBase = import.meta.env.MODE === 'development'
  ? ''
  : import.meta.env.VITE_API_URL?.replace(/\/$/, '') || ''

const cargarOpciones = async () => {
  try {
    isLoading.value = true
    errorMsg.value = null
    const url = `${apiBase}/api/v1/usuarios/perfiles`
    console.log('Solicitando perfiles desde:', url)
    const response = await fetch(url)

    if (!response.ok) {
      throw new Error(`Error al obtener los datos: ${response.status} ${response.statusText}`)
    }

    const data = await response.json()
    console.log('Perfiles API response:', data)

    if (Array.isArray(data)) {
      opciones.value = data
    } else if (Array.isArray(data?.data)) {
      opciones.value = data.data
    } else {
      opciones.value = []
      errorMsg.value = 'No se encontraron perfiles válidos.'
    }

    if (!opciones.value.length && !errorMsg.value) {
      errorMsg.value = 'No hay perfiles disponibles.'
    }
  } catch (error) {
    errorMsg.value = 'No se pudieron cargar las opciones.'
    console.error('Error cargando perfiles:', error)
  } finally {
    isLoading.value = false
  }
}

const searchQuery = ref('')

const abrirModal = () => {
  mostrarModal.value = true
  cargarOpciones()
}

onMounted(() => {
  cargarOpciones()
  obtieneUsuarios()
})

const resetForm = () => {
  form.value = {
    name: '',
    user: '',
    password: '',
    repeatPass: '',
    idPerfil: '',
    photo: null,
    photoName: '',
    photoType: '',
  }
  selectedFile.value = null
  previewUrl.value = null
}

//post de formulario 
const handleSubmit = async () => {
  cargando.value = true
  mensajeExito.value = ''

  try {
    const response = await fetch('/api/v1/usuarios/guarda', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        ...form.value,
        photo: form.value.photo,
        photoName: form.value.photoName,
        photoType: form.value.photoType,
      }),
    })

    if (!response.ok) throw new Error('Error en el servidor')

    const data = await response.json()
    mensajeExito.value = `¡Registro exitoso! ID: ${data.id}`
    resetForm()
  } catch (error) {
    console.error('Error post-servicio:', error)
  } finally {
    cargando.value = false
  }
}

const usuarios = ref([])

const filteredData = computed(() => {
  if (!searchQuery.value) return usuarios.value
  return usuarios.value.filter(item => {
    const query = searchQuery.value.toLowerCase()
    return [item.nombre, item.user, item.perfil]
      .filter(Boolean)
      .some(value => value.toLowerCase().includes(query))
  })
})

const obtieneUsuarios = async () => {
  try {
    const response = await fetch('/api/v1/usuarios/consultaTodos')
    if (!response.ok) throw new Error('Error al obtener usuarios')
    
    const data = await response.json()
    const lista = Array.isArray(data) ? data : data?.data ?? []

    // Mapeamos los usuarios para agregar la URL de la imagen formateada
    usuarios.value = lista.map(usuario => ({
      ...usuario,
      photoUrl: usuario.photo ? `data:image/jpeg;base64,${usuario.photo}` : null
    }))

  } catch (error) {
    console.error('Error obteniendo usuarios:', error)
    usuarios.value = []
  }
}
</script>

<template>
  <div class="dashboard">



    <!-- Search and Table -->
    <div class="content-section">
      <h2>Administrar Usuarios</h2>
      <div class="container">
        <!-- Botón para abrir el popup -->
        <button class="btn-open" @click="abrirModal">
          Alta de usuario
        </button>

        <!-- Fondo oscuro y ventana emergente -->
        <div v-if="mostrarModal" class="modal-overlay" @click.self="mostrarModal = false">
          <div class="modal-content">
            <header class="form-header">
              <div>
                <p class="form-subtitle">Panel de Gestión</p>
                <h2>Formulario de Contacto</h2>
              </div>
            </header>
            <form @submit.prevent="handleSubmit">
              <div class="inputs-row">
                <input class="inputs-row__input" v-model="form.name" placeholder="Nombre completo" />
                <input class="inputs-row__input" v-model="form.user" placeholder="Usuario" />
              </div>

              <div class="inputs-row">
                <input class="inputs-row__input" :type="showPassword ? 'text' : 'password'" id="password"
                  v-model="form.password" placeholder="Ingresa tu contraseña" />
                <input class="inputs-row__input" :type="showPassword ? 'text' : 'password'" id="password2"
                  v-model="form.repeatPass" placeholder="Repite tu contraseña" />
              </div>

              <div class="inputs-row">
                <div class="upload-wrapper">
                  <input type="file" accept="image/*" @change="handleFileUpload" />

                 

                  <label for="combo-list">Escoge el perfil</label>

                  <!-- Estado de Carga -->
                  <p v-if="isLoading">Cargando opciones...</p>

                  <!-- Estado de Error -->
                  <p v-else-if="errorMsg" class="error">{{ errorMsg }}</p>

                  <!-- Select / Combo List -->
                  <select v-else id="combo-list" v-model="form.idPerfil" class="inputs-row__input">
                    <option value="" disabled>-- Selecciona una opción --</option>
                    <option v-for="item in opciones" :key="item.id ?? item.perfil" :value="item.id ?? item.perfil">
                      {{ item.perfil ?? item.name ?? item.label ?? 'Opción' }}
                    </option>
                  </select>



                </div>
              </div>
              <div class="inputs-row">
                <!-- Botón para cerrar -->
                <button class="btn-guardar" type="submit" :disabled="cargando">
                  {{ cargando ? 'Guardando...' : 'Guardar' }}
                  Guardar
                </button>

                <button class="btn-close" @click="mostrarModal = false">
                  Cerrar
                </button>
              </div>
            </form>
          </div>
        </div>

        <table class="data-table">
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Perfil</th>
            <th>Foto</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(usuario, index) in filteredData" :key="index">
            <td>{{ usuario.nombre }}</td>
            <td>{{ usuario.perfil }}</td>
            <td><img 
            v-if="usuario.photo" 
            :src="`data:image/jpeg;base64,${usuario.photo}`" 
            alt="Foto de usuario" 
            class="imagen-pequena"
          />
          <span v-else>Sin foto</span></td>
          </tr>
        </tbody>
      </table>
      </div>
    </div>
  </div>
</template>
