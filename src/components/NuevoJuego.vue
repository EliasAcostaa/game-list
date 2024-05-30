<template>
    <h3>Nuevo Juego</h3>
    <div class="formulario">
        <form id="juego">
            <div>
                <label for="nombre">Nombre del Juego </label>
                <input type="text" name="nombre" v-model="juego.nombreJ">
                <p v-show=validName style="color: red;">el nombre no debe ser vacio</p>
            </div>
            <div>
                <label for="plataforma">Plataforma </label>
                <select name="plataforma" id="platform" v-model="juego.plataforma">
                    <option value="PC" selected>PC</option>
                    <option value="PlayStation">PlayStation</option>
                    <option value="Xbox One">Xbox One</option>
                </select>
            </div>
            <div>
                <label for="Estado">Estado </label>
                <select name="Estado" id="state" v-model="juego.estado">
                    <option value="Pendiente" selected>Pendiente</option>
                    <option value="Jugando">Jugando</option>
                    <option value="Completado">Completado</option>
                </select>
            </div>
            <div>
                <label for="puntaje">Puntaje </label>
                <input type="text" name="puntaje" v-model="juego.puntaje">
                <p v-show=validRating style="color: red;">el puntaje debe estar entre 1 y 10</p>
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
        plataforma: 'PC',
        estado: 'Pendiente',
        puntaje: ''
    })

    const emitEvent = defineEmits(["AddGame"])

    const handleAdd = () => {
        if(!validName.value && !validRating.value){
            emitEvent("add-game", {...juego.value})
            juego.value.nombreJ = ''
            juego.value.puntaje = ''
        }
        
    }

    const validName = computed(() => { return juego.value.nombreJ.trim() == ''})

    const validRating = computed(() => { return juego.value.puntaje < 1 || juego.value.puntaje > 10 })
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