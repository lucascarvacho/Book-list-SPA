<template>
  <div class="listaLibros">
    <h2>TU LISTA DE LIBROS</h2>

    <div class="filtros">
      <select v-model="campoFiltro">
        <option value="ninguno">Ninguno</option>
        <option value="titulo">Título</option>
        <option value="autor">Autor</option>
        <option value="genero">Género</option>
      </select>
      <input v-model="textoBusqueda" type="text" placeholder="Buscar..." @keyup.enter="confirmarBusqueda">
    </div>

    <div class="libros">
      <LibroAgregado
        v-for="libro in librosFiltrados"
        :key="libro.id"
        :libro="libro"
        @eliminar="eliminarLibro"
      />
      <p v-if="librosFiltrados.length === 0">No se encontraron libros.</p>
    </div>

    <button class="btn-primario" @click="mostrarFormulario = true">Agregar libro</button>
  </div>

  <FormularioLibro
    v-if="mostrarFormulario"
    @guardar="agregarLibro"
    @cancelar="mostrarFormulario = false"
  />
</template>

<script setup>
import { inject, ref, computed } from 'vue'
import LibroAgregado from '../components/LibroAgregado.vue'
import FormularioLibro from '../components/FormularioLibro.vue'

const libros = inject('libros')
const mostrarFormulario = inject('mostrarFormulario')
const agregarLibro = inject('agregarLibro')
const eliminarLibro = inject('eliminarLibro')

const campoFiltro = ref('ninguno')
const textoBusqueda = ref('')

const librosFiltrados = computed(() => {
  if (campoFiltro.value === 'ninguno' || textoBusqueda.value.trim() === '') {
    return libros.value
  }

  const texto = textoBusqueda.value.toLowerCase()

  return libros.value.filter(libro => {
    const valor = String(libro[campoFiltro.value] || '').toLowerCase()
    return valor.includes(texto)
  })
})

function confirmarBusqueda () {
  console.log(`Buscando "${textoBusqueda.value}" en el campo "${campoFiltro.value}"`)
}
</script>
