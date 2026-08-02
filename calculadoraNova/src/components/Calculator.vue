<script setup>
import {ref} from 'vue';

const current = ref("");
const operator = ref(null);
const previous = ref(null);
const operatorClicked = ref(false);
const clear = () => {
  current.value = ""
}

const sign = () => { //ACRESCENTA O SINAL DE - NA FRENTE
  current.value = current.value.charAt(0) === '-' ? current.value.slice(1) : `-${current.value}`;
}

const percent = () => {
  current.value = `${parseFloat(current.value) / 100}`
}

const append = (number) => {
  if (operatorClicked.value) {
    current.value = ''
    operatorClicked.value = false
  }
  current.value = `${current.value}${number}` //irá adicionando o n° no fim da string
}

const dot = () => {
  if (current.value.indexOf('.') === -1) {
    append.value('.')
  }
}

const setPrevious = () => {
  previous.value = current.value;
  operatorClicked.value = true;
}

const divide = () => {
  operator.value = (a, b) => a / b
  setPrevious()
}

const times = () => {
  operator.value = (a, b) => a * b
  setPrevious()
}

const minus = () => {
  operator.value = (a, b) => a - b
  setPrevious()
}

const add = () => {
  operator.value = (a, b) => a + b
  setPrevious()
}

const equal = () => {
  current.value = `${operator.value(parseFloat(current.value), parseFloat(previous.value))}`
  previous.value = null;
}
</script>

<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click='append(7)' class="btn">7</div>
    <div @click='append(8)' class="btn">8</div>
    <div @click='append(9)' class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click='append(4)' class="btn">4</div>
    <div @click='append(5)' class="btn">5</div>
    <div @click='append(6)' class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click='append(1)' class="btn">1</div>
    <div @click='append(2)' class="btn">2</div>
    <div @click='append(3)' class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click='append(0)' class="zero btn">0</div>
    <div @click="dot()" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr); /** 4 colunas com a mesma fração de espaço */
  grid-auto-rows: minmax(50px, auto); /** espaçamento entre as linhas de 50px, auto para centralizar no espaço disponibilizado */
}

.display {
  grid-column: 1 /5; /** Dizendo quantas colunas o item irá usar */
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #999;
  border: 1px solid #333;
}

.operator {
  background-color: orange;
  color: white;
}

</style>
