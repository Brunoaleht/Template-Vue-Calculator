<template>
  <div id="App">
    <h1>Calculadora</h1>
    <CalculatorCalc />
  </div>
</template>

<script>
import CalculatorCalc from "./main/Calculator.vue";
export default {
  name: "App",
  components: {
    CalculatorCalc,
  },
};
</script>

<style>
* {
  font-family: monospace;
}
body {
  margin: 0;
}
#App {
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  text-align: center;
  align-items: center;
  color: #fff;
  background: linear-gradient(to right, rgb(83, 105, 118), rgb(41, 46, 73));
}
</style>
