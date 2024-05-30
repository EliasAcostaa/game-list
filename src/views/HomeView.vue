<template>
  <div class="home">
    <div id="titulo">
      <h1>Administración de Videojuegos</h1>
    </div>
    <div>
      <NuevoJuego @add-game="AddGame"/>
    </div>
    <div id="listaJuegos">
        <table>
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Plataforma</th>
                    <th>Estado</th>
                    <th>Puntaje</th>
                    <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="juego of juegos" :key="juego.nombreJ">
                    <td>{{ juego.nombreJ }}</td>
                    <td>{{ juego.plataforma }}</td>
                    <td>{{ juego.estado }}</td>
                    <td>{{ juego.puntaje }}</td>
                    <td><button @click="abrirModal(juego)">Mas Info</button>
                        <ModalInfo :visible="showModal" :juego="juegoActual" @update:visible="showModal = $event" />
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
  </div>
</template>

<script setup>
  import {  ref } from 'vue';
  import NuevoJuego from '@/components/NuevoJuego.vue';
  import ModalInfo from '@/components/InfoModalComponent.vue'

  let juegos = ref([])
  let showModal = ref(false)

  const juegoActual = ref({
  nombreJ: '',
  plataforma: '',
  estado: '',
  puntaje: ''
  })

  function AddGame(juego){
    juegos.value.push(juego)
  }

  const abrirModal = (juego) => {
    juegoActual.value = {...juego}
    showModal.value = true
  }
</script>
