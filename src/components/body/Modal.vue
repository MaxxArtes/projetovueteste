<!-- Modal.vue -->
<template>
    <div class="modal" v-if="showModal">
      <div class="modal-content">
        <slot></slot>
        <button @click="closeModal">Fechar</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Modal",
    data() {
      return {
        showModal: false
      };
    },
    methods: {
      closeModal() {
        this.showModal = false;
      }
    }
  };
  </script>
  
  <style scoped>
  /* Adicione estilos do modal aqui */
  .modal {
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
  }
  </style>
  