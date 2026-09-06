<template>
  <div class="card-libro">
    <p><strong>ID: {{ libro.id }}</strong></p>
    <h3>{{ libro.titulo }}</h3>
    <p>{{ libro.autor }}</p>
    <router-link :to="`/libros/${libro.id}`">
      <button class="btn-primario">Ver</button>
    </router-link>
    <button class="btn-secundario" @click="$emit('eliminar', libro.id)">Eliminar</button>
  </div>
</template>

<script setup>
defineProps(['libro'])
defineEmits(['eliminar'])
</script>
