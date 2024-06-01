<template>

  <!-- BLOQUE DE ICONO 1!!!!!  -->
  <img id="imagen1" src="../assets/mando-de-juegos.gif" alt="icono">

  <!-- BLOQUE DE ICONO 2!!!  -->
  <img id="imagen2" src="../assets/consola-de-videojuegos.gif" alt="icono">


  <div class="home">
    <div id="titulo">
      <h1>Administración de Videojuegos</h1>
    </div>

    <div id="CuadroJuegoNuevo">  <!-- id de CuadroJuegoNuevo, realizar cuadro de css  -->
      <NuevoJuego id="NuevoJuego" @add-game="AddGame"/>
    </div>
    
    <div id="Filtros">
      <label id="idNombre" for="Nombre">Nombre</label>
      <input id="txtNombre" type="text" name="Nombre" v-model="nombreF">
      <label id="idPlataforma" for="Plataforma">Plataforma</label>
      <input id="txtPlataforma" type="text" name="Plataforma" v-model="plataformaF">
      <label id="idEstado" for="Estado">Estado</label>
      <input id="txtEstado" type="text" name="Estado" v-model="EstadoF">
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

<script id="script" setup>
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



<style scoped>

.home {
  display: flex;
  justify-content: center;
  align-items: center;      
  display: grid;
  grid-template-columns: 3(1fr);
  background-color:#cd96db;  /* color de todo el home */ 
}

body {
  background-color: #5a2168;  /* no funciona el color para TODA la pagina????? */
}
  
  #Filtros {
    color: rgb(10, 15, 78);
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    font-weight: 200px;
    border: 8px solid #272269;
    right: 5%;
  }

  #txtNombre,
  #txtPlataforma,
  #txtEstado {
    padding: 0.5rem;
  }

#titulo {
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  width: 30rem;
  margin-left: 7rem;
  margin-top: 30px;
}


#CuadroJuegoNuevo {
  width: 30rem;
  border: 14px solid #272269;
  padding: 50px;
  margin: 55px;
  background-image: linear-gradient(to right, #95509bce , #db4ea0);
}


#listaJuegos {
  padding: 5rem;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}



/* ICONOS PROPIEDADES */

#imagen1 {
  border-radius: 70%;
  opacity: 0.9;
  position: absolute;
  left: 100px;
  width: 300px;
  border: 5px solid #040c58;
  padding: 2px;
  top: 9rem;
  
}


#imagen2 {
  border-radius: 70%;
  opacity: 0.9;
  position: absolute;
  right: 100px;
  width: 300px;
  border: 5px solid #040c58;
  padding: 2px;
  top: 9rem;
}




/* PROPIEDADES TABLA / RESULTADOS*/ 

table {
  border-collapse: collapse;
  width: 100%;
  background-color: rgba(146, 23, 146, 0.5); /* For browsers that do not support gradients */
  background-image: linear-gradient(to right, rgba(233, 73, 225, 0.541) , rgba(131, 51, 177, 0.575));
}

th, td {
  padding: 10px;
  text-align: left;
  border: 2px solid #000000;
}



</style>
