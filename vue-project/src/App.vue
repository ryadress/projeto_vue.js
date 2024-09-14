<script setup>
import { ref, watch } from 'vue';

// Definindo as variáveis reativas
const numero1 = ref(0);
const numero2 = ref(0);
const operacao = ref('+');
const resultado = ref(null);

// Função para calcular o resultado
function calcular() {
  const n1 = numero1.value;
  const n2 = numero2.value;
  switch (operacao.value) {
    case '+':
      resultado.value = n1 + n2;
      break;
    case '-':
      resultado.value = n1 - n2;
      break;
    case '*':
      resultado.value = n1 * n2;
      break;
    case '/':
      resultado.value = n2 !== 0 ? n1 / n2 : 'Erro: Divisão por zero';
      break;
    default:
      resultado.value = null;
  }
}

// Observadores para atualizar o cálculo quando os valores mudam
watch(numero1, calcular);
watch(numero2, calcular);
watch(operacao, calcular);
</script>

<template>
  <div id="app">
    <h1>Calculadora Aritmética</h1>
    <div class="calculator">
      <input v-model.number="numero1" type="number" placeholder="Número 1" />
      <select v-model="operacao">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
      </select>
      <input v-model.number="numero2" type="number" placeholder="Número 2" />
    </div>
    <div v-if="resultado !== null">
      <h2>Resultado: {{ resultado }}</h2>
    </div>
  </div>
</template>

<style scoped>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  margin: 50px auto;
  max-width: 400px;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

h1 {
  color: #333;
  margin-bottom: 20px;
}

.calculator {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input,
select {
  font-size: 16px;
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;
}

input[type="number"] {
  width: calc(50% - 20px);
  display: inline-block;
  margin-right: 10px;
}

select {
  width: calc(30% - 20px);
  display: inline-block;
  margin: 0 10px;
}

h2 {
  color: #007BFF;
  font-size: 24px;
  margin-top: 20px;
}

</style>
