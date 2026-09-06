<template>
  <div class="overlay">
    <div class="modal">
      <h3>Agregar un nuevo libro</h3>

      <form @submit.prevent="guardar">
        <label>Título del Libro</label>
        <input v-model="form.titulo" type="text">

        <label>Autor</label>
        <input v-model="form.autor" type="text">

        <label>Género</label>
        <select v-model="form.genero">
          <option>Novela</option>
          <option>Cuento</option>
          <option>Poesía</option>
          <option>Drama</option>
          <option>Romance</option>
          <option>Terror</option>
          <option>Misterio</option>
          <option>Policial</option>
          <option>Thriller</option>
          <option>Ciencia ficción</option>
          <option>Fantasía</option>
          <option>Aventura</option>
          <option>Histórica</option>
          <option>Distopía</option>
          <option>Biografía</option>
          <option>Autobiografía</option>
          <option>Filosofía</option>
          <option>Ensayo</option>
          <option>Humor</option>
          <option>Drama psicológico</option>
          <option>Juvenil</option>
          <option>Infantil</option>
          <option>Erótica</option>
          <option>Religión</option>
          <option>Política</option>
          <option>Autoayuda</option>
          <option>Educación</option>
          <option>Historia</option>
          <option>Ciencia</option>
          <option>Viajes</option>
          <option>Gastronomía</option>
          <option>Arte</option>
        </select>

        <label>Subgénero</label>
        <select v-model="form.subgenero">
          <option>Novela histórica</option>
          <option>Novela romántica</option>
          <option>Cuento fantástico</option>
          <option>Cuento de terror</option>
          <option>Poesía lírica</option>
          <option>Poesía romántica</option>
          <option>Romance contemporáneo</option>
          <option>Romance histórico</option>
          <option>Terror psicológico</option>
          <option>Terror sobrenatural</option>
          <option>Misterio policial</option>
          <option>Misterio detectivesco</option>
          <option>Novela detectivesca</option>
          <option>Novela negra</option>
          <option>Thriller psicológico</option>
          <option>Thriller policial</option>
          <option>Cyberpunk</option>
          <option>Space opera</option>
          <option>Fantasía épica</option>
          <option>Fantasía oscura</option>
          <option>Aventura histórica</option>
          <option>Aventura de exploración</option>
          <option>Historia antigua</option>
          <option>Historia contemporánea</option>
          <option>Biografía histórica</option>
          <option>Autobiografía</option>
          <option>Filosofía política</option>
          <option>Existencialismo</option>
          <option>Ensayo filosófico</option>
          <option>Ensayo político</option>
          <option>Cuentos infantiles</option>
          <option>Fantasía infantil</option>
          <option>Desarrollo personal</option>
          <option>Productividad</option>
        </select>

        <label>Año</label>
        <input v-model="form.anio" type="number">

        <label>Mini resumen</label>
        <textarea v-model="form.resumen"></textarea>

        <button class="btn-primario" type="submit">Agregar Libro</button>
        <button class="btn-secundario" type="button" @click="$emit('cancelar')">Cancelar</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['guardar', 'cancelar'])

const form = reactive({
  titulo: '',
  autor: '',
  genero: '',
  subgenero: '',
  anio: '',
  resumen: ''
})

function guardar () {
  emit('guardar', { ...form })
}
</script>
