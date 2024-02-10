<script setup lang="ts">
import { ref } from 'vue'
import type { Ref } from 'vue'

import CharactersData from '@/Data/CharactersContent';

const emits = defineEmits(['NewOc']);

const name: Ref<string> = ref('Prueba2')
const lastname: Ref<string> = ref('Prueba1')
const age: Ref<number> = ref(0)
const personality: Ref<string> = ref('Prueba1')
const occupation: Ref<string> = ref('Prueba1')
const hobby: Ref<string> = ref('Prueba1')
const pet: Ref<string> = ref('Prueba1')
const likes: Ref<string> = ref('Prueba1')
const dislikes: Ref<string> = ref('Prueba1')
const preciousobject: Ref<string> = ref('Prueba1')

const nuevoOC = {
    id: CharactersData.length + 1,
    name: name.value,
    lastname: lastname.value,
    age: age.value,
    personality: personality    .value,
    occupation: occupation.value,
    hobby: hobby.value,
    pet: pet.value,
    likes: likes.value,
    dislikes: dislikes.value,
    preciousobject: preciousobject.value
}

const clicked=() =>{
    emits('NewOc', nuevoOC)
}

</script>

<template>
  <main>
    <div :class="{ 'formulario': true }">
      <h1>Formulario VUE</h1>
      <button @click="clicked()"></button>
    </div>
  </main>
</template>

<style scoped>
.formulario {
  width: 100%;
  height: auto;
  padding: 2rem 0rem 2rem 0rem;
  display: flex;
  flex-direction: column;
  background-color: rgba(242, 243, 235, 0.705);
  border: 5px solid rgb(54, 53, 52);
  align-items: center;
  text-align: left;
}

.formulario h1 {
  font-size: 2rem;
  color: rgb(54, 53, 52);
}

.formulario input {
  height: 2rem;
  width: 90%;
  padding-left: 10px;
  margin-top: 2rem;
  letter-spacing: 1px;
  background: none;
  border: 0px none rgb(70, 58, 46);
  border-bottom: 2px solid rgb(70, 58, 46);
  color: rgb(109, 84, 58);
}

.formulario input::placeholder {
  color: rgb(109, 84, 58);
  text-transform: uppercase;
}

.formulario input:focus {
  outline: none;
}

.formulario p {
  padding-left: 0;
  font-size: 18px;
  color: red;
}

.formulario button {
  margin-top: 2rem;
  height: 3rem;
  width: 12rem;
  border: 0px none;
  border-radius: 5px;
  background-color: rgb(182, 141, 98);
  text-transform: uppercase;
  color: rgb(255, 255, 255);
}

.formulario button:disabled {
  cursor: not-allowed;
}

.formulario button:enabled:hover {
  cursor: pointer;
}

.formulario button:enabled:active {
  background-color: rgb(134, 99, 60);
}

.select_form input {
  height: 1rem;
  width: 2rem;
}

.select_form label {
  font-size: 20px;
  height: 2rem;
  color: aliceblue;
  margin-right: 2rem;
}
</style>