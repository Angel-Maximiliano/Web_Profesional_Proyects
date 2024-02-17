<script setup lang="ts">
  import {ref} from 'vue'
  import type {Ref} from 'vue'

  const name:Ref<string> = ref('')
  const last_name:Ref<string> = ref('')
  const age:Ref<number> = ref(0)
  const gender = ref('')
  const other_gender:Ref<string> = ref('')
  const button:Ref<boolean>=ref(false)


  const errors = ref ({
      name: '',
      last_name:'',
      age:'',
      other_gender: '',
    });

  const validation = () => {
  if (name.value.length > 18 || name.value.length < 5){
    errors.value.name = 'El nombre debe tener entre 5 y 18 caracteres.'
  }else{
    errors.value.name = ''
  }

  if (last_name.value === name.value){
    errors.value.last_name = 'El apellido no debe ser igual al nombre'
  }else{
    errors.value.last_name = ''
  }

  if (age.value <=  0){
    errors.value.age = 'La edad debe ser mayor a 0'
  }else if(age.value >= 60){
    errors.value.age = 'La edad debe ser menor a 60'
  }else{
    errors.value.age = ' '
  }

  if (other_gender.value.length <= 0 || other_gender.value.trim() == ''){
    errors.value.other_gender = 'Ingresa un dato correcto'
  } else {
    errors.value.other_gender = ' '
  }

}
</script>

<template>
  <main> 
    <div :class="{'formulario':true}" @input="validation()">

      <h1>Formulario VUE</h1>
      <input v-model="name" type="text" placeholder="Mis nombres">
      <p v-if="errors.name">{{ errors.name }}</p>
      <input v-model="last_name" type="text" placeholder="Mis apellidos">
      <p v-if="errors.last_name">{{ errors.last_name }}</p>
      <input  v-model="age" type="number">
      <p v-if="errors.age">{{ errors.age }}</p>

      <div :class="{'select_form':true}">
        <input type="radio" id="masculino" value="Masculino" v-model="gender">
        <label for="masculino">Masculino</label>
        <input type="radio" id="femenino" value="Femenino" v-model="gender">
        <label for="femenino">Femenino</label>
        <input type="radio" id="otro" value="Otro" v-model="gender">
        <label for="otro">Otro</label>
      </div>

        <input v-if="gender.includes('Otro')" v-model="other_gender" type="text" placeholder="Ejem: No binario">
        <p v-if="errors.other_gender && gender.includes('Otro')">{{ errors.other_gender }}</p>

      <button :disabled="name.length <= 0">Enviar</button>

    </div>
  </main>
</template>

<style scoped>

.formulario{
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

.formulario h1{
  font-size: 2rem;
  color: rgb(54,53,52);
}

.formulario input{
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

.formulario input::placeholder{
  color: rgb(109, 84, 58);
  text-transform: uppercase;
}

.formulario input:focus{
  outline: none;
}

.formulario p{
  padding-left: 0;
  font-size: 18px;
  color: red;
}

.formulario button{
  margin-top: 2rem;
  height: 3rem;
  width: 12rem;
  border: 0px none;
  border-radius: 5px;
  background-color: rgb(182, 141, 98);
  text-transform: uppercase;
  color: rgb(255,255,255);
}

.formulario button:hover{
  cursor: pointer;
}

.formulario button:active{
  background-color: rgb(134, 99, 60);
}

.select_form input{
  height: 1rem;
  width: 2rem;
}
.select_form label{
font-size: 20px;
height: 2rem;
color: aliceblue;
margin-right: 2rem;
}
</style>