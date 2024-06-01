<template>
    <h3>Nuevo Juego</h3>
    <div class="formulario">
        <form id="juego">
            <div id="nombre">
                <label style="color: white" for="nombre">Juego </label> <!-- colores de texto modificados desde aca -->
                <input id="inputNombre" type="text" name="nombre" v-model="juego.nombreJ">
                <p id="IngreseSuJuego" v-show=invalidName style="color: darkblue">¡Ingrese su juego!</p>
            </div>
            <div id="plataforma">
                <label style="color: white" for="plataforma">Plataforma </label>
                <select name="plataforma" id="platform" v-model="juego.plataforma">
                    <option value="" disabled selected>PC | PlayStation | Xbox One</option>
                    <option value="PC">PC</option>
                    <option value="PlayStation">PlayStation</option>
                    <option value="">Xbox One</option>
                </select>
            </div>
            <div id="estado">
                <label style="color: white" for="Estado">Estado </label>
                <select name="Estado" id="state" v-model="juego.estado">
                    <option value="" disabled selected>Pendiente | Jugando | Completado</option>
                    <option value="Pendiente">Pendiente</option>
                    <option value="Jugando">Jugando</option>
                    <option value="Completado">Completado</option>
                </select>
            </div>
            <div id="puntaje">
                <label style="color: white" for="puntaje">Puntaje </label>
                <input id="inputPuntaje" type="number" name="puntaje" v-model="juego.puntaje">
                <p v-show=invalidRating style="color: red;">el puntaje debe estar entre 1 y 10</p>
            </div>
            <div>
                <button id="boton" type="button" @click="handleAdd()"><span>Registrar Videojuego</span></button>
            </div>
        </form>
    </div>
    
</template>

<script setup>
    import { ref, computed, defineEmits } from 'vue'

    let juego = ref({
        nombreJ: '',
        plataforma: '',
        estado: '',
        puntaje: ''
    })

    const emitEvent = defineEmits(["AddGame"])

    const handleAdd = () => {
        if(!invalidName.value && !invalidRating.value && !invalidOption.value){
            emitEvent("add-game", {...juego.value})
            juego.value.nombreJ = ''
            juego.value.plataforma = '',
            juego.value.estado = '',
            juego.value.puntaje = ''
        }
    }

    const invalidOption = computed(() => { return (juego.value.plataforma === '' || juego.value.estado === '')})

    const invalidName = computed(() => { return juego.value.nombreJ.trim() === ''})

    const invalidRating = computed(() => { return juego.value.puntaje !== '' && (juego.value.puntaje < 1 || juego.value.puntaje > 10);})
</script>



<style scoped>


#juego{
    display: flex;
    flex-direction: column;
    align-items: flex-start; 
}

h3 {
    font-size: 150%;
    margin-top: 1rem;
    margin-bottom: 1rem;
}

#juego {
    align-items: center;
    align-content: center;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    padding: 1rem;
}

#nombre,
#plataforma,
#estado,
#puntaje {
    font-size: 120%;
    padding: 1rem;
}

#inputNombre,
#platform,
#state,
#inputPuntaje {
    padding: 0.5rem;
}

#plataforma {
    padding: 1rem;
}

#platform,
#state{
    width: 14rem;
}


#IngreseSuJuego {
    padding-top: 1rem;
    margin-top: 0rem;       /* PROPIEDADES ALERTA INGRESE SU JUEGO */
    margin-bottom: -1rem;
}


/* PROPIEDADES DEL BOTON REGISTRAR VIDEOJUEGO */

#boton {
  display: inline-block;
  border-radius: 4px;
  background-color: #084e5f93;
  color: #ffffff;
  text-align: center;
  font-size: 19px;
  padding: 20px;
  width: 300px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

#boton {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.6s;
}

#boton:after {
  content: '\00bb';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -10px;
  transition: 0.5s;
}

#boton:hover {
  padding-right: 100px;
}

#boton:hover:after {
  opacity: 1;
  right: 3rem;
  margin-top: 0rem;
  font-size: 3rem;
}

</style>