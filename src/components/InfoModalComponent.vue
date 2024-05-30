<!-- Modal.vue -->
<template>
    <div v-if="visible" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <h2>{{ props.juego.nombreJ }}</h2>
        <p>Plataforma: {{ props.juego.plataforma }}</p>
        <p>Estado: {{ props.juego.estado }}</p>
        <p>Puntaje: {{ props.juego.puntaje }}</p>
        <button @click="closeModal">Cerrar</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue'
  
  const props = defineProps({
    visible: {
      type: Boolean,
      required: true
    },
    juego: {
      type: Object,
      required: true
    }
  })
  
  const emitEvent = defineEmits(['update:visible'])
  
  const closeModal = () => {
    emitEvent('update:visible', false)
  }
  </script>
  
  <style scoped>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal-content {
    background: white;
    padding: 20px;
    border-radius: 5px;
    min-width: 300px;
    position: relative;
  }
  </style>
  