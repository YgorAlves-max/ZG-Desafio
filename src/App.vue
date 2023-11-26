<script setup lang="ts">
import axios from 'axios';
import { ref } from 'vue';

const fazerRequisicao = async () => {
  try {

    const nomeCompleto = 'YgorAlvesFerreiradosSantos';
    const email = 'ygorpb2@gmail.com';
    const cpf = '020.995.886-35';

    if (!nomeCompleto || !email || !cpf) {
      console.error('Parâmetros incompletos. Certifique-se de fornecer nome, email e cpf.');
      return;
    }

    const url = `https://tranquil-rex-405218.rj.r.appspot.com/hashCodeServer?nome=${nomeCompleto}&email=${email}&cpf=${cpf}`;

    const response = await axios.post(url);

    console.log('Resposta do servidor:', response.data);
  } catch (error) {
    console.error('Erro ao fazer a requisição:', error);
  }

};
const anos = ref<number>(0);
const meses = ref<number>(0);
const dias = ref<number>(0);
const idadeCalculada = ref<number | null>(null);

const calcularIdade = () => {
  idadeCalculada.value = (anos.value * 365) + (meses.value * 30) + dias.value;
};
</script>

<template>
  <div class="logo">
    <div>
      <h2>Requisição para o desafio!</h2>
      <button @click="fazerRequisicao">Fazer Requisição</button>
    </div>
    <div class="divisor"></div>
    <div class="div1">
      <h3 class="title">Calculadora de Idade em Dias</h3>
      <form @submit.prevent="calcularIdade">
        <label for="anos">Anos:</label>
        <input type="number" v-model="anos" required />

        <label for="meses">Meses:</label>
        <input type="number" v-model="meses" required />

        <label for="dias">Dias:</label>
        <input type="number" v-model="dias" required />

        <button type="submit">Calcular Idade</button>
      </form>

      <div v-if="idadeCalculada !== null">
        <p>A idade da pessoa em dias é: {{ idadeCalculada }} dias.</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 30px;
  padding: auto;
  text-align: center;
  transition: 300ms;
}

.divisor {
  width: 100%;
  margin-top: 20px;
  border-bottom: 1px solid #ccc;
  /* Cor e estilo da borda inferior */
}

.div1 {
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 10px;
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.title {
  color: #42b883;
}

form {
  max-width: 400px;
  width: 100%;
  display: flex;
  flex-direction: column;
  margin-top: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  margin-bottom: 10px;
}

button {
  background-color: #42b883;
  color: white;
  padding: 10px;
  cursor: pointer;
}
</style>
