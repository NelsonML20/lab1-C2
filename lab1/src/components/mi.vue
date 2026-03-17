<template>
  <div class="container">
    <header class="hero">
      <h1>{{ titulo }}</h1>
      <p>{{ subtitulo }}</p>
    </header>

    <main class="grid">
      <section class="card">
        <h2>Registrar tutoría</h2>

        <form @submit.prevent="registrarSolicitud">
          <div class="field">
            <label>Nombre</label>
            <input type="text" v-model.trim="nombre" />
          </div>

          <div class="field">
            <label>Materia</label>
            <input type="text" v-model.trim="materia" />
          </div>

          <div class="field">
            <label>Modalidad</label>
            <select v-model="modalidad">
              <option value="">Seleccione</option>
              <option>Presencial</option>
              <option>Virtual</option>
            </select>
          </div>

          <div class="field">
            <label>Fecha</label>
            <input type="date" v-model="fecha" :min="fechaMinima" />
          </div>

          <div class="field">
            <label>Descripción</label>
            <textarea v-model.trim="descripcion"></textarea>
          </div>

          <button :disabled="bloquearBoton">
            Guardar
          </button>
        </form>

        <div v-if="errores.length" class="alert error">
          <ul>
            <li v-for="(e, i) in errores" :key="i">{{ e }}</li>
          </ul>
        </div>

        <p v-if="mensajeExito" class="alert success">
          {{ mensajeExito }}
        </p>
      </section>

      <section class="card">
        <h2>Solicitudes</h2>

        <input
          placeholder="Filtrar por materia"
          v-model.trim="filtroMateria"
        />

        <div v-if="solicitudesFiltradas.length === 0" class="empty-state">
          No hay datos
        </div>

        <div v-else>
          <div v-for="s in solicitudesFiltradas" :key="s.id" class="solicitud">
            <h3>{{ s.nombre }}</h3>
            <p><strong>Materia:</strong> {{ s.materia }}</p>
            <p><strong>Modalidad:</strong> {{ s.modalidad }}</p>
            <p><strong>Fecha:</strong> {{ s.fecha }}</p>
            <p><strong>Descripción:</strong> {{ s.descripcion }}</p>

            <button @click="cambiarEstado(s.id)">
              {{ s.estado }}
            </button>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const titulo = ref('Tutorías UGB')
const subtitulo = ref('Sistema de tutorías académicas')

const nombre = ref('')
const materia = ref('')
const modalidad = ref('')
const fecha = ref('')
const descripcion = ref('')
const filtroMateria = ref('')

const errores = ref([])
const mensajeExito = ref('')
const solicitudes = ref([])

const fechaMinima = computed(() => {
  return new Date().toISOString().split('T')[0]
})

const bloquearBoton = computed(() => {
  return (
    !nombre.value ||
    !materia.value ||
    !modalidad.value ||
    !fecha.value ||
    !descripcion.value
  )
})

const solicitudesFiltradas = computed(() => {
  return solicitudes.value.filter(s =>
    s.materia.toLowerCase().includes(filtroMateria.value.toLowerCase())
  )
})

function validar() {
  errores.value = []
  mensajeExito.value = ''

  if (!nombre.value) errores.value.push('Nombre requerido')
  if (!materia.value) errores.value.push('Materia requerida')
  if (!modalidad.value) errores.value.push('Modalidad requerida')
  if (!fecha.value) errores.value.push('Fecha requerida')
  if (fecha.value && fecha.value < fechaMinima.value) {
    errores.value.push('La fecha no puede ser anterior a hoy')
  }
  if (!descripcion.value || descripcion.value.length < 10) {
    errores.value.push('Descripción mínima de 10 caracteres')
  }

  return errores.value.length === 0
}

function registrarSolicitud() {
  if (!validar()) return

  const nueva = {
    id: Date.now(),
    nombre: nombre.value,
    materia: materia.value,
    modalidad: modalidad.value,
    fecha: fecha.value,
    descripcion: descripcion.value,
    estado: 'Pendiente'
  }

  solicitudes.value.push(nueva)
  errores.value = []
  mensajeExito.value = 'Guardado correctamente'
  limpiar()
}

function cambiarEstado(id) {
  const s = solicitudes.value.find(x => x.id === id)
  if (s) {
    s.estado = s.estado === 'Pendiente' ? 'Atendida' : 'Pendiente'
  }
}

function limpiar() {
  nombre.value = ''
  materia.value = ''
  modalidad.value = ''
  fecha.value = ''
  descripcion.value = ''
}
</script>

<style scoped>
.container {
  width: 92%;
  max-width: 1200px;
  margin: 30px auto;
}

.hero {
  background: linear-gradient(135deg, #0f172a, #1d4ed8);
  color: white;
  padding: 30px;
  border-radius: 18px;
  margin-bottom: 25px;
}

.hero h1 {
  font-size: 2rem;
  margin-bottom: 10px;
}

.grid {
  display: grid;
  grid-template-columns: 1fr 1.1fr;
  gap: 20px;
}

.card {
  background: white;
  border-radius: 18px;
  padding: 20px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.field {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input,
select,
textarea {
  width: 100%;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

button {
  padding: 10px;
  border: none;
  border-radius: 8px;
  background: #2563eb;
  color: white;
  cursor: pointer;
}

button:disabled {
  background: gray;
  cursor: not-allowed;
}

.solicitud {
  border: 1px solid #ddd;
  padding: 10px;
  margin-top: 10px;
  border-radius: 10px;
}

.alert {
  margin-top: 15px;
  padding: 12px;
  border-radius: 10px;
}

.error {
  background: #fee2e2;
  color: #991b1b;
}

.success {
  background: #dcfce7;
  color: #166534;
}

.empty-state {
  margin-top: 10px;
  padding: 12px;
  border: 1px dashed #ccc;
  border-radius: 10px;
  text-align: center;
}

@media (max-width: 900px) {
  .grid {
    grid-template-columns: 1fr;
  }
}
</style>