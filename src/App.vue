<template>
  <main>

<div class="header">
  <div class="marca">
    <img src="./assets/logo.png" alt="" class="logo">
    <h1>Book List SPA</h1>
  </div>
  <nav>
    <router-link to="/">Inicio</router-link>
    <router-link to="/libros">Mis libros</router-link>
  </nav>
</div>

  <router-view />

  <div class="footer">
    <p>Contacto: lucas.carvacho.utem10@gmail.com
</p>
  </div>

  </main>
</template>

<script setup>
import { ref, provide } from 'vue'

const libros = ref([])
const mostrarFormulario = ref(false)
const nombrePerfil = ref('Tú')
const fotoPerfil = ref('')

function agregarLibro (nuevoLibro) {
  libros.value.push({
    id: libros.value.length + 1,
    ...nuevoLibro
  })
  mostrarFormulario.value = false
}

function eliminarLibro (id) {
  libros.value = libros.value.filter(libro => libro.id !== id)
}

function editarLibro (id, datosActualizados) {
  const libro = libros.value.find(l => l.id === id)
  if (libro) {
    Object.assign(libro, datosActualizados)
  }
}

provide('libros', libros)
provide('mostrarFormulario', mostrarFormulario)
provide('agregarLibro', agregarLibro)
provide('eliminarLibro', eliminarLibro)
provide('editarLibro', editarLibro)
provide('nombrePerfil', nombrePerfil)
provide('fotoPerfil', fotoPerfil)
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Segoe UI', Arial, sans-serif;
  background-color: #4a4a4a;
  color: white;
}

/* Header */
.header {
  background-color: #4a4a4a;
  color: white;
  padding: 1rem 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
}

.header h1 {
  margin: 0;
  font-size: 1.5rem;
}

.header nav {
  display: flex;
  gap: 1rem;
}

.header nav a {
  color: white;
  text-decoration: none;
  font-weight: 600;
  padding: 0.4rem 0.8rem;
  border-radius: 6px;
  transition: background-color 0.2s;
}

.header nav a:hover {
  background-color: rgb(255, 92, 209);
}

.header .logo {
  height: 40px;
  width: auto;
  object-fit: contain;
}

.header .marca {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

/* Sección 1 - Inicio */
.seccion1 {
  background-color: rgba(255, 255, 255, 0.15);
  padding: 2rem;
  margin: 1.5rem;
  border-radius: 10px;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 2rem;
  flex-wrap: wrap;
}

.columna-izquierda {
  flex: 1;
  min-width: 250px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 0.8rem;
}

.columna-izquierda p {
  max-width: 500px;
}

.botones {
  display: flex;
  gap: 0.8rem;
}

.seccion1 .bienvenida {
  max-width: 250px;
  width: 100%;
  height: auto;
  border-radius: 8px;
}

.seccion1 h2 {
  margin: 0;
}

.seccion1 button {
  align-self: flex-start;
}

/* Lista de libros */
.listaLibros {
  padding: 1.5rem 2rem;
  margin: 1.5rem;
}

.listaLibros h2 {
  margin-top: 0;
}

.filtros {
  display: flex;
  gap: 0.8rem;
  margin-bottom: 1.5rem;
}

.filtros select,
.filtros input {
  padding: 0.5rem 0.8rem;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 0.95rem;
}

.filtros input {
  flex: 1;
}

.libros {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
  margin-bottom: 1.5rem;
}

/* Card de libro */
.card-libro {
  background-color: #464646;
  border-radius: 8px;
  border: 2px solid white;
  padding: 1rem 1.2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.card-libro h3 {
  margin: 0.2rem 0;
}

.card-libro > div:first-child {
  flex: 1;
}

/* Botones generales */
button {
  border: none;
  padding: 0.6rem 1.2rem;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.95rem;
  font-weight: bold;
  transition: background-color 0.2s;
}

.btn-primario {
  background-color: rgb(236, 1, 169);
  color: white;
  border: 2px solid rgb(236, 1, 169);
}

.btn-primario:hover {
  background-color: rgb(255, 92, 209);
  border: 2px solid rgb(255, 92, 209);
}

.btn-secundario {
  background-color: transparent;
  color: white;
  border: 2px solid white;
}

.btn-secundario:hover {
  background-color: #777;
  border: 2px solid white;
}

/* Card de perfil */
.card-perfil {
  background-color: #464646;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  cursor: pointer;
  max-width: 200px;
}

.foto-perfil {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 0.5rem;
}

/* Modal / formulario */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal {
  background-color: #4a4a4a;
  border-radius: 10px;
  padding: 2rem;
  width: 90%;
  max-width: 420px;
  max-height: 90vh;
  overflow-y: auto;
}

.modal h3 {
  margin-top: 0;
}

.modal form {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.modal label {
  font-size: 0.85rem;
  font-weight: 600;
  margin-bottom: -0.4rem;
}

.modal input,
.modal select,
.modal textarea {
  padding: 0.6rem;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 0.95rem;
  font-family: inherit;
}

.modal textarea {
  min-height: 80px;
  resize: vertical;
}

.modal form > div {
  display: flex;
  gap: 0.6rem;
  margin-top: 0.5rem;
}

/* Detalle de libro */
.detalle-libro {
  background-color: #464646;
  border: 2px solid white;
  margin: 1.5rem;
  padding: 2rem;
  border-radius: 10px;
}

.detalle-libro h2 {
  margin-top: 0;
}

/* Footer */
.footer {
  background-color: #4a4a4a;
  color: white;
  text-align: center;
  padding: 1rem;
  margin-top: 2rem;
}
</style>
