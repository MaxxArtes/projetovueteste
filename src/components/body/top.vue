<template>
  <section :style="estiloComponente" class="tecnologias-section">
    <h2 class="title">Cadastrar tecnologias</h2>
    <!-- Formulário para cadastrar tecnologias -->
    <div class="form">
      <input
        v-model="tecnologia"
        type="text"
        class="input"
        placeholder="Digite a tecnologia"
        @keyup.enter="cadastrarTecnologia"
      />
      <button @click="cadastrarTecnologia" class="btn">Cadastrar</button>
    </div>

    <!-- Lista de tecnologias cadastradas -->
    <ul class="tecnologias-list">
      <li
        v-for="(tec, index) in tecnologias"
        :key="index"
        class="tecnologia-item"
      >
        <span class="tecnologia">{{ index + 1 }}</span>
        {{ tec }}
        <!-- Botões para editar e deletar tecnologia -->
        <div>
          <button @click="editarTecnologia(index)" class="btn-atualizar">
            Editar
          </button>
          <button @click="deletarTecnologia(index)" class="btn-deletar">
            Deletar
          </button>
        </div>
      </li>
    </ul>

    <!-- Modal para editar tecnologia -->
    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <p>Editar tecnologia {{ tecnologiaSelecionada + 1 }}</p>
        <input
          type="text"
          v-model="tecnologia"
          placeholder="Digite a Tecnologia atualizada"
        />
        <!-- Botões dentro do modal -->
        <button @click="confirmarEdicao" class="btn-editar">Editar</button>
        <button @click="fecharModal" class="btn-fechar">Fechar</button>
      </div>
    </div>

    <!-- Outros elementos (menu, search) -->
    <div class="menu"></div>
    <div class="search"></div>
  </section>
</template>


<script>
import axios from "axios";

export default {
  name: "TecnologiasSection",
  props: ["estiloComponente"],
  data() {
    return {
      // Estado do modal e dados das tecnologias
      showModal: false,
      tecnologia: "",
      tecnologias: JSON.parse(localStorage.getItem("tecnologia")) || [],
      axios,
      tecnologiaSelecionada: null,
      // estiloComponente: {
      //   display: "none",
      // },
    };
  },
  methods: {
    // Método para abrir o modal
    openModal() {
      this.showModal = true;
    },

    // Método para fechar o modal
    fecharModal() {
      this.showModal = false;
    },

    // Método para cadastrar tecnologia
    cadastrarTecnologia() {
      if (!this.tecnologia.trim()) {
        alert("Digite o nome da tecnologia antes de cadastrar.");
        return;
      }

      if (this.tecnologiaSelecionada !== null) {
        // Atualiza a tecnologia existente
        this.tecnologias[this.tecnologiaSelecionada] = this.tecnologia;
        this.tecnologiaSelecionada = null;
      } else {
        // Adiciona uma nova tecnologia
        this.tecnologias.push(this.tecnologia);
      }

      localStorage.setItem("tecnologia", JSON.stringify(this.tecnologias));
      this.tecnologia = "";
      this.showModal = false; // Fecha o modal após cadastrar/Atualizar
    },

    // Método para deletar tecnologia
    deletarTecnologia(index) {
      this.tecnologias.splice(index, 1);
      localStorage.setItem("tecnologia", JSON.stringify(this.tecnologias));
    },

    // Método para editar tecnologia
    editarTecnologia(index) {
      // Define a tecnologia selecionada para edição
      this.tecnologia = this.tecnologias[index];
      this.tecnologiaSelecionada = index;
      this.showModal = true; // Abre o modal ao editar
    },

    // Método para confirmar a edição no modal
    confirmarEdicao() {
      if (!this.tecnologia.trim()) {
        alert("Digite o nome da tecnologia antes de editar.");
        return;
      }

      // Atualiza a tecnologia existente
      this.tecnologias[this.tecnologiaSelecionada] = this.tecnologia;
      localStorage.setItem("tecnologia", JSON.stringify(this.tecnologias));
      this.tecnologia = "";
      this.tecnologiaSelecionada = null;
      this.showModal = false; // Fecha o modal após editar
    },
  },
};
</script>


<style scoped>
/* ... (seu estilo existente) */

/* Estilos específicos para o modal */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);  /* Fundo preto semi-transparente para cobrir a tela */
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;  /* Cor de fundo branca para o conteúdo do modal */
  padding: 20px;
  border-radius: 5px;  /* Borda arredondada */
}

/* Estilos para os botões dentro do modal */
.btn-fechar {
  background-color: #ccc;  /* Cor de fundo cinza claro */
  color: #000;  /* Cor do texto preto */
  border: none;
  padding: 5px 10px;
  border-radius: 5px;  /* Borda arredondada */
  cursor: pointer;
  margin-top: 10px;
  transition: background-color 0.3s ease;  /* Transição suave de cor ao passar o mouse */
}

.btn-fechar:hover {
  background-color: #999;  /* Cor de fundo cinza um pouco mais escura ao passar o mouse */
}

.btn-atualizar {
  background-color: #4da6ff;  /* Cor de fundo azul claro */
  color: #ffffff;  /* Cor do texto branco */
  border: none;
  padding: 5px 10px;
  border-radius: 50px;  /* Borda arredondada para um botão circular */
  cursor: pointer;
  margin-left: 10px;
  transition: background-color 0.3s ease;  /* Transição suave de cor ao passar o mouse */
}

.btn-atualizar:hover {
  background-color: #0077ff;  /* Cor de fundo azul mais intensa ao passar o mouse */
}

.btn-editar {
  background-color: #ccc;  /* Cor de fundo cinza claro */
  color: #000;  /* Cor do texto preto */
  border: none;
  padding: 5px 10px;
  border-radius: 5px;  /* Borda arredondada */
  cursor: pointer;
  margin-top: 10px;
  transition: background-color 0.3s ease;  /* Transição suave de cor ao passar o mouse */
}

/* Estilos para a seção de tecnologias */
.tecnologias-section {
  margin-left: 10px;
  margin-right: 10px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);  /* Cor de fundo branca */
  color: #000000;  /* Cor do texto preto */
  padding: 20px;
  font-size: 18px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  text-transform: uppercase;
  border-bottom-left-radius: 15px;  /* Borda arredondada no canto inferior esquerdo */
  border-bottom-right-radius: 15px;  /* Borda arredondada no canto inferior direito */
}

.title {
  justify-content: center;
  text-align: center;
  color: #ffffff;
  font-size: 24px;
  margin-bottom: 15px;
}

.form {
  justify-content: center;
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.input {
  height: 35px;
  margin-right: 10px;
  border-radius: 5px;  /* Borda arredondada */
  border: 1px solid #000000;
  color: #000000;
  background-color: #ffffff;  /* Cor de fundo branca */
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  text-transform: uppercase;
  padding: 5px 10px;
}

.btn {
  border-radius: 5px;  /* Borda arredondada */
  border: 1px solid #000000;
  color: #000000;
  background-color: #ffffff;  /* Cor de fundo branca */
  text-transform: uppercase;
  cursor: pointer;
  padding: 5px 10px;
}

.tecnologias-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.tecnologia-item {
  max-width: 300px;
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 10px;
  margin: 0 10px 10px 10px;
  background-color: #f0f0f0;  /* Cor de fundo cinza claro */
  border-radius: 50px;  /* Borda arredondada para um formato mais circular */
}

.btn-deletar {
  background-color: #ff4d4d;  /* Cor de fundo vermelho claro */
  color: #ffffff;  /* Cor do texto branco */
  border: none;
  padding: 5px 10px;
  border-radius: 50px;  /* Borda arredondada para um botão circular */
  cursor: pointer;
  transition: background-color 0.3s ease;  /* Transição suave de cor ao passar o mouse */
}

.btn-deletar:hover {
  background-color: #ff0000;  /* Cor de fundo vermelho mais intensa ao passar o mouse */
}
</style>

