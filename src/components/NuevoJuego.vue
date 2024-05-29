<template>
    <h3>Nuevo Juego</h3>
    <div class="formulario">
        <form id="juego">
            <div>
                <label for="nombre">Nombre del Juego </label>
                <input type="text" name="nombre">
            </div>
            <div>
                <label for="plataforma">Plataforma </label>
                <select name="plataforma" id="platform">
                    <option value="PC" selected>PC</option>
                    <option value="PlayStation">PlayStation</option>
                    <option value="Xbox One">Xbox One</option>
                </select>
            </div>
            <div>
                <label for="Estado">Estado </label>
                <select name="Estado" id="state">
                    <option value="Pendiente" selected>Pendiente</option>
                    <option value="Jugando">Jugando</option>
                    <option value="Completado">Completado</option>
                </select>
            </div>
            <div>
                <label for="puntaje">Puntaje </label>
                <input type="text" name="puntaje">
            </div>
            <div>
                <input type="button" value="Registrar Videojuego">
            </div>
        </form>
    </div>
</template>

<script>
    import { defineComponent } from "vue";

    export default defineComponent({
        name: 'NuevoJuego'
    })
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