<template>
  <div class="home">
    <div id="titulo">
      <h1>Administración de Videojuegos</h1>
    </div>
    <div>
      <NuevoJuego />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NuevoJuego from '@/components/NuevoJuego.vue'

export default {
  name: 'HomeView',
  components: {
    NuevoJuego
  },
  data() {
    return {
      Juegos: []
    }
  },
}
</script>
