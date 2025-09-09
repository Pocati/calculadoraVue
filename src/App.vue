<script setup>
import { ref, computed } from "vue"

const numero1 = ref(0)
const numero2 = ref(0)
const operacao = ref("soma")

const resultado = computed(() => {
  switch (operacao.value) {
    case "soma":
      return numero1.value + numero2.value
    case "subtracao":
      return numero1.value - numero2.value
    case "multiplicacao":
      return numero1.value * numero2.value
    case "divisao":
      return numero2.value !== 0 ? (numero1.value / numero2.value).toFixed(2) : "Erro (divisão por zero)"
    default:
      return 0
  }
})
</script>

<template>
  <div id="app" class="container">
    <h1>🧮 Calculadora com VueJS</h1>

    <div class="calculadora">
      <input type="number" v-model.number="numero1" placeholder="Digite o primeiro número" />

      <input type="number" v-model.number="numero2" placeholder="Digite o segundo número" />

      <select v-model="operacao">
        <option value="soma">+</option>
        <option value="subtracao">-</option>
        <option value="multiplicacao">×</option>
        <option value="divisao">÷</option>
      </select>

      <p class="resultado">Resultado: <strong>{{ resultado }}</strong></p>
    </div>
  </div>
</template>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background: #f6f6f6;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 400px;
  margin: 50px auto;
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

input,
select {
  display: block;
  width: 100%;
  padding: 8px;
  margin: 10px 0;
  border-radius: 8px;
  border: 1px solid #ddd;
  font-size: 16px;
}

.resultado {
  margin-top: 20px;
  font-size: 20px;
}
</style>
