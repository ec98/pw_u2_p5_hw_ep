<template>
  <div>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Calculadora></Calculadora>
    <!-- es incomodo tener el problema, asi que le puse div para evitar ese problema tan molestoso. -->
  </div>
</template>

<script>
import Calculadora from "./components/Calculadora.vue";

export default {
  name: "App",
  components: {
    Calculadora
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
