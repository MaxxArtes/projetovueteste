<template>
  <div>
    <h1 class="header"></h1>
    <div class="container">
      <div class="nav">
        <img class="logo" :src="imagem" alt="" />
        <div class="menu">
          <button class="btn" @click="navigate('home')">{{ nav[0] }}</button>
          <button class="btn" @click="alterarEstiloComponente">{{ nav[1] }}</button>
          <button class="btn" @click="openContato">{{ nav[2] }}</button>
        </div>
        <contato :open="open" />
        <div class="search">
          <input type="text" class="input" placeholder="Pesquisar" />
        </div>
      </div>
      <div class="content" style="display: flex">
        <img :src="imagem" alt="" style="width: 50%" />
        <img :src="imagem" alt="" style="width: 50%" />
      </div>
    </div>
  </div>
</template>

<script>
import TecnologiasSection from "../body/top.vue";
import Contato from "./contato.vue";
import { ref } from "vue";

export default {
  data() {
    return {
      nav: ["Home", "Sobre", "Contato"],
      open: ref(false),
      imagem: "/img/moveis.jpg",
    };
  },
  components: {
    Contato,
    TecnologiasSection,
  },
  methods: {
    openContato() {
      this.open = !this.open;
    },

    alterarEstiloComponente() {
      // Emita um evento para notificar o componente alvo sobre a mudança
      this.$emit('alterar-estilo-componente');
      
    },
  },
};
</script>

<style scoped>
.logo {
  margin-right: 10px;
  margin-left: 110px;
  width: 3%;
  height: 3%;
  border-radius: 50%;
}
</style>
