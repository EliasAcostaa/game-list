<template>
    <h3>Nuevo Juego</h3>
    <div class="formulario">
        <form id="juego">
            <div>
                <label for="nombre">Nombre del Juego </label>
                <input type="text" name="nombre" v-model="juego.nombreJ">
                <p v-show=invalidName style="color: red;">el nombre no debe ser vacio</p>
            </div>
            <div>
                <label for="plataforma">Plataforma </label>
                <select name="plataforma" id="platform" v-model="juego.plataforma">
                    <option value="" disabled selected>PC | PlayStation | Xbox One</option>
                    <option value="PC">PC</option>
                    <option value="PlayStation">PlayStation</option>
                    <option value="">Xbox One</option>
                </select>
            </div>
            <div>
                <label for="Estado">Estado </label>
                <select name="Estado" id="state" v-model="juego.estado">
                    <option value="" disabled selected>Pendiente | Jugando | Completado</option>
                    <option value="Pendiente">Pendiente</option>
                    <option value="Jugando">Jugando</option>
                    <option value="Completado">Completado</option>
                </select>
            </div>
            <div>
                <label for="puntaje">Puntaje </label>
                <input type="number" name="puntaje" v-model="juego.puntaje">
                <p v-show=invalidRating style="color: red;">el puntaje debe estar entre 1 y 10</p>
            </div>
            <div>
                <input type="button" @click="handleAdd()" value="Registrar Videojuego">
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

h3{
    display: flex;
    align-items: flex-start;
}

</style>