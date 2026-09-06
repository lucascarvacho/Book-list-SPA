<template>
  <div class="seccion1">

    <div class="columna-izquierda">
      <h2>¿Cómo funciona Book List SPA?</h2>
      <img src="../assets/inicio.png" alt="" class="bienvenida">
      <p>Aquí puedes agregar tus libros favoritos, verlos en detalle, editarlos o eliminarlos cuando quieras. Todo se organiza en tu lista personal, disponible en la sección "Mis libros".</p>
      <p>{{ tip }}</p>
      <div class="botones">
        <button class="btn-primario" @click="mostrarFormulario = true">Agregar libro</button>
        <button class="btn-secundario" @click.once="mostrarTip">Ver consejo</button>
      </div>
    </div>

    <CardPerfil :cantidad="libros.length" />

  </div>

  <FormularioLibro
    v-if="mostrarFormulario"
    @guardar="agregarLibro"
    @cancelar="mostrarFormulario = false"
  />
</template>

<script setup>
import { inject, ref } from 'vue'
import CardPerfil from '../components/CardPerfil.vue'
import FormularioLibro from '../components/FormularioLibro.vue'

const libros = inject('libros')
const mostrarFormulario = inject('mostrarFormulario')
const agregarLibro = inject('agregarLibro')

const tip = ref('')

function mostrarTip () {
  tip.value = 'Consejo: puedes filtrar tus libros por género, título o autor en la sección de lista.'
}
</script>
