<template>
  <div class="card-perfil">

    <div v-if="!editando" @click="iniciarEdicion">
      <img :src="foto || placeholder" alt="Foto de perfil" class="foto-perfil">
      <p>{{ nombre }}</p>
      <p>Libros agregados: {{ cantidad }}</p>
    </div>

    <div v-else>
      <img :src="fotoTemp || placeholder" alt="Foto de perfil" class="foto-perfil">
      <input type="file" accept="image/*" @change="cambiarFoto">

      <input v-model="nombreTemp" type="text" placeholder="Tu nombre">

      <button class="btn-primario" @click="guardar">Guardar</button>
      <button class="btn-secundario" @click="cancelar">Cancelar</button>
    </div>

  </div>
</template>

<script setup>
import { inject, ref } from 'vue'

defineProps(['cantidad'])

const placeholder = 'https://via.placeholder.com/80?text=Tú'

const nombre = inject('nombrePerfil')
const foto = inject('fotoPerfil')

const editando = ref(false)
const nombreTemp = ref('')
const fotoTemp = ref('')

function iniciarEdicion () {
  nombreTemp.value = nombre.value
  fotoTemp.value = foto.value
  editando.value = true
}

function cambiarFoto (evento) {
  const archivo = evento.target.files[0]
  if (archivo) {
    fotoTemp.value = URL.createObjectURL(archivo)
  }
}

function guardar () {
  nombre.value = nombreTemp.value
  foto.value = fotoTemp.value
  editando.value = false
}

function cancelar () {
  editando.value = false
}
</script>
