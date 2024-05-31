<template>
  <div class="home">
    <div id="titulo">
      <h1>Administración de Videojuegos</h1>
    </div>
    <div>
      <NuevoJuego @add-game="AddGame"/>
    </div>
    <div id="Filtros">
      <label for="Nombre">Nombre</label>
      <input type="text" name="Nombre" v-model="nombreF">
      <label for="Plataforma">Plataforma</label>
      <input type="text" name="Plataforma" v-model="plataformaF">
      <label for="Estado">Estado</label>
      <input type="text" name="Estado" v-model="EstadoF">
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
                <tr v-for="juego of filtrados" :key="juego.nombreJ">
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
  import {  ref, computed } from 'vue';
  import NuevoJuego from '@/components/NuevoJuego.vue';
  import ModalInfo from '@/components/InfoModalComponent.vue'

  let juegos = ref([])
  let showModal = ref(false)
  let nombreF = ref('')
  let plataformaF = ref('')
  let EstadoF = ref('')

  let filtrados = computed(() => {
    return juegos.value.filter(juego => {
      return (
        (nombreF.value === '' || juego.nombreJ.toLowerCase().includes(nombreF.value.toLowerCase().trim())) &&
        (plataformaF.value === '' || juego.plataforma.toLowerCase().includes(plataformaF.value.toLowerCase().trim())) &&
        (EstadoF.value === '' || juego.estado.toLowerCase().includes(EstadoF.value.toLowerCase().trim()))
      )
    })
  })

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
