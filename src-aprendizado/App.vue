<script setup>
import { reactive } from 'vue';

const nome = "Guerino"
const meuObj = {
  nome: "Guerino",
  filmeFavorito: "Top Gun"
}


function dizOla(){
  return `${nome} diz oi`
}

const meuIcon = "https://static.lms.ebaconline.com.br/avatars/8ef28de4-fa44-4c21-87d3-bfba5aede385/100x100.webp"
const botaoOff = false

const isTheFox = true
const isTheFox2 = false

const estautorizado = true


// let contador = 0
const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['nome1', 'nome2', 'nome3'],
  nomeAInserir: ''
})

function incrementar(){
  estado.contador++
}

function subtrair(){
  estado.contador--
}

function alteraEmail(e){
  estado.email = e.target.value
}

function mostraSaldoFuturo(){
  const { saldo, transferindo } = estado
  return saldo - transferindo
}

function validaValorT(){
  const { saldo, transferindo } = estado
  return saldo >= transferindo
}

function cadastraNome(){
  const {nomes, nomeAInserir} = estado
  if(nomeAInserir.length > 3){
    nomes.push(nomeAInserir)
  } else{
    alert('Dgite mais caracteres')
  }
}



</script>

<template>
  <h1>{{ nome }}</h1>
  <h1>{{ dizOla() }}</h1>
  <h1>{{ meuObj.filmeFavorito }}</h1>
  <img v-if="isTheFox" :src="meuIcon" alt="">
  <img v-else-if="isTheFox2" :src="meuIcon" alt="">
  <h2 v-else>is not the fox</h2>

  <h1 v-if="estautorizado">Bem vindo</h1>
  <h1 v-else>Nao aut</h1>

  <button :disabled="botaoOff">enviar</button>
  <hr>
  <br>
  {{ estado.contador }}
  <button @click="incrementar" type="button">+</button>
  <button @click="subtrair" type="button">-</button>
  <br>

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail">

  <br>
  <hr>

  Saldo: {{ estado.saldo }} <br>
  Transferido: {{ estado.transferindo }}<br>
  Saldo depois da ttransferencia: {{ mostraSaldoFuturo() }}<br>
  <input class="campo" :class="{ invalido: !validaValorT() }" @keyup="e => estado.transferindo = e.target.value" type="number" placeholder="Quantia" name="" id="">
  <button v-if="validaValorT()">Transferir</button>
  <span v-else>Valorémaior que o saldo</span>


  <br>
  <hr>

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="e => estado.nomeAInserir = e.target.value" type="text">
  <button @click="cadastraNome">cadastrar nome</button>

</template>

<style scoped>
img{
  max-width: 200px;
}

.campo{
  border: 2px solid black
}
.invalido{
  border-color: red;
  outline-color: red;
}

</style>
