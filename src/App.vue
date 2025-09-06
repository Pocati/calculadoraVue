<script setup>
import { ref } from 'vue'

const numeroAtual = ref('0')          // número exibido na tela
const primeiroValor = ref(null)       // primeiro número
const operador = ref(null)            // operador atual (+ - * /)
const esperandoSegundo = ref(false)   // flag: aguardando digitar o segundo número

// Limpa tudo
const clear = () => {
  numeroAtual.value = '0'
  primeiroValor.value = null
  operador.value = null
  esperandoSegundo.value = false
}

// Inverte sinal
const sinal = () => {
  if (numeroAtual.value !== '0') {
    numeroAtual.value = numeroAtual.value.startsWith('-')
      ? numeroAtual.value.slice(1)
      : '-' + numeroAtual.value
  }
}

// Porcentagem
const porcent = () => {
  numeroAtual.value = (parseFloat(numeroAtual.value) / 100).toString()
}

// Adicionar número no display
function append(number) {
  if (numeroAtual.value === '0' || esperandoSegundo.value) {
    numeroAtual.value = number
    esperandoSegundo.value = false
  } else {
    numeroAtual.value += number
  }
}

// Adicionar ponto decimal
function ponto() {
  if (!numeroAtual.value.includes('.')) {
    numeroAtual.value += '.'
  }
}

// Selecionar operador
function escolherOperador(op) {
  primeiroValor.value = parseFloat(numeroAtual.value)
  operador.value = op
  esperandoSegundo.value = true
}

// Calcular resultado
const igual = () => {
  if (operador.value === null || primeiroValor.value === null) return

  const segundo = parseFloat(numeroAtual.value)
  let resultado = 0

  switch (operador.value) {
    case '+':
      resultado = primeiroValor.value + segundo
      break
    case '-':
      resultado = primeiroValor.value - segundo
      break
    case '*':
      resultado = primeiroValor.value * segundo
      break
    case '/':
      resultado = segundo !== 0 ? primeiroValor.value / segundo : 'Erro'
      break
  }

  numeroAtual.value = resultado.toString()
  operador.value = null
  primeiroValor.value = null
}
</script>

<template>
  <header class="cabecalho">
    <h1>🧮 Calculadora com VueJS</h1>
  </header>

  <div class="calculadora">
    <div class="display">{{ numeroAtual }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sinal" class="btn">+/-</div>
    <div @click="porcent" class="btn">%</div>
    <div @click="escolherOperador('/')" class="btn operadores">/</div>

    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="escolherOperador('*')" class="btn operadores">x</div>

    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="escolherOperador('-')" class="btn operadores">-</div>

    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="escolherOperador('+')" class="btn operadores">+</div>

    <div @click="append('0')" class="btn zero">0</div>
    <div @click="ponto" class="btn operadores">.</div>
    <div @click="igual" class="btn operadores">=</div>
  </div>
</template>

<style scoped>

.cabecalho {
  text-align: center;
  margin-bottom: 20px;
  background: linear-gradient(90deg, #ff8c00, #ff4500);
  color: white;
  padding: 15px 30px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.3);
  animation: fadeIn 1s ease-in-out;
}

.cabecalho h1 {
  margin: 0;
  font-size: 28px;
  font-weight: bold;
}

.calculadora {
  text-align: center;
  height: 400px;
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1/5;
  background-color: black;
  color: white;
  padding: 10px;
  text-align: right;
}

.zero {
  grid-column: 1/3;
}

.btn {
  cursor: pointer;
  background-color: #f2f2f2;
  border: 1px solid #333;
  display: flex;
  align-items: center;
  justify-content: center;
}

.operadores {
  background-color: orange;
}
</style>
