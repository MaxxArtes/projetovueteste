  <script>
import headss from "./components/head/nav.vue";
import top from "./components/body/top.vue";

export default {
  name: "App",
  components: {
    headss,
    top,
  },
  data() {
    return {
      estiloComponente: {
        display: "block",
      },
    };
  },
  methods: {
    alterarEstiloComponente() {
      console.log("teste");
      if (this.estiloComponente.display === 'block') {
        this.estiloComponente.display = 'none';
      }
      else {
        this.estiloComponente.display = 'block';        
      }
    }
  },
};
</script>

<template>
  <div>
    <div>
      <headss @alterar-estilo-componente="alterarEstiloComponente"/>
    </div>
    <div>
      <top :estilo-componente="estiloComponente"/>
    </div>
    <div>
    </div>
  </div>
</template>

<style>

.content {
  position: relative;
  z-index: -1;
}
.top {
  background: #000000;
}

header{
  width: 100vw !important;
  height: 100vh;
  margin-top: 0;
  margin-bottom: 0;
  padding: 0;
  margin-left: 0;
  margin-right: 0;
}

.header {
  width: 100%;
  margin: 0;
  text-align: center;
  font-size: 30px;
  font-weight: 300;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: #000000;
}

.nav {
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0;
  margin: 0;
  list-style-type: none;
  background-color: #292929;
}

.nav .btn:hover {
  background-color: #000000;
  color: #ffffff;
}

.btn {
  height: 30px;
  padding: 20px, 10px, 20px, 10px;
  margin: 10px;
  border-radius: 5px;
  border: 1px solid #ffffff;
  color: #ffffff;
  background-color: transparent;
  cursor: pointer;
  font-size: 10px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 300;
  text-align: center;
  justify-content: center;
  align-items: center;
  transition: 0.3s;
}

.menu {
width: 100%;
}

.container {
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  width: 100%;
  height: 60px;
  background-color: #000000;
}

.search input{
  margin-right: 110px;
  width: 200px;
  height: 20px;
  border: 1px solid #000000;
  padding: 5px 10px;
  border-radius: 5px;
  outline: none;
  color: #000000;
  font-size: 10px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 300;
  background-color: #ffffff;
}

.search input[type="text"]:focus {
  border: 1px solid #292929;
  border-radius: 5px;
  background-color: #ffffff;
  transition: 0.3s;
}

.contato {
  margin-right: 5px;
  width: 200px;
  height: 30px;
  border: 1px solid #d30101;
  padding: 5px 10px;
  border-radius: 5px;
  outline: none;
  color: #a30505;
  font-size: 10px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 300;
  background-color: #ffffff;
}

</style>
