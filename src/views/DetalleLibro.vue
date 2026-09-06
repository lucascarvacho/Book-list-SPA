<template>
  <div class="detalle-libro" v-if="libro">

    <div v-if="!editando">
      <h2>{{ libro.titulo }}</h2>
      <p>Autor: {{ libro.autor }}</p>
      <p>Género: {{ libro.genero }}</p>
      <p>Subgénero: {{ libro.subgenero }}</p>
      <p>Año: {{ libro.anio }}</p>
      <p>Mini resumen:</p>
      <p>{{ libro.resumen }}</p>

      <router-link to="/libros">
        <button class="btn-primario">Volver</button>
      </router-link>
      <button class="btn-secundario" @click="iniciarEdicion">Editar</button>
    </div>

    <div v-else>
      <h3>Editar libro</h3>

      <label>Título del Libro</label>
      <input v-model="form.titulo" type="text">

      <label>Autor</label>
      <input v-model="form.autor" type="text">

      <label>Género</label>
      <select v-model="form.genero">
        <option>Ciencia ficción</option>
        <option>Fantasía</option>
        <option>Terror</option>
      </select>

      <label>Subgénero</label>
      <select v-model="form.subgenero">
        <option>Cyberpunk</option>
        <option>Distopía</option>
      </select>

      <label>Año</label>
      <input v-model="form.anio" type="number">

      <label>Mini resumen</label>
      <textarea v-model="form.resumen"></textarea>

      <button class="btn-primario" @click="guardarCambios">Guardar</button>
      <button class="btn-secundario" @click="editando = false">Cancelar</button>
    </div>

  </div>

  <div v-else>
    <p>Libro no encontrado.</p>
    <router-link to="/libros">Volver</router-link>
  </div>
</template>

<script setup>
import { inject, computed, ref, reactive } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const libros = inject('libros')
const editarLibro = inject('editarLibro')

const libro = computed(() =>
  libros.value.find(l => l.id === Number(route.params.id))
)

const editando = ref(false)

const form = reactive({
  titulo: '',
  autor: '',
  genero: '',
  subgenero: '',
  anio: '',
  resumen: ''
})

function iniciarEdicion () {
  Object.assign(form, libro.value)
  editando.value = true
}

function guardarCambios () {
  editarLibro(libro.value.id, { ...form })
  editando.value = false
}
</script>
