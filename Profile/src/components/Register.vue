<template>

    <div class="Contenedor">
        <div class="Formulario" @input="validacion()">
            <form @submit.prevent="Ingreso">

                <h1>Registrarse</h1>

                <input type="text" v-model="nombre" placeholder="Nombre">
                <input type="text" v-model="apellido" placeholder="Apellido">
                <input type="email" v-model="correo" placeholder="Correo">
                <input type="text" v-model="contraseña" placeholder="Contraseña">

                <button :disabled="habilitado">Registrar</button>
            </form>
        </div>
    </div>

</template>

<script setup lang="ts">

import ObjectUser from './Data/DataUsuarios'
import type { IUser } from './Interfaces/InterUsuarios';

import {ref} from 'vue'


const nombre = ref('')
const apellido = ref('')
const correo = ref('')
const contraseña = ref('')
const habilitado = ref(true)

const Usuarios = ref<IUser[]>(ObjectUser);

const validacion = () =>{
    if( nombre.value.trim() != '' && apellido.value.trim() != ''  && correo.value.trim() != '' && contraseña.value.trim() != ''){
        habilitado.value = false
    }else{
        habilitado.value = true
    }
}

const Ingreso = () =>{
    if(Usuarios.value.some((user) => user.email === correo.value)){
        alert('El correo ya se ha registraddo')
        return
    }

    const NewUser: IUser = {
        id: ObjectUser.length + 1,
        name: nombre.value,
        lastname: apellido.value,
        email: correo.value,
        password: contraseña.value
    }

    Usuarios.value.push(NewUser)
    alert("Te has registrado correctamente")

    nombre.value= ''
    apellido.value= ''
    correo.value = ''
    contraseña.value = ''
}

</script>

<style scoped>

    .Contenedor {
        display: flex;
        justify-content: center;
        /* background-color: rgba(88, 27, 124, 0.336); */
    }

    .Formulario {
        width: 50%;
        padding: 3rem 0px 3rem 0px;
        margin-top: 3rem;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgba(247, 245, 238, 0.863);
        border: 8px solid rgb(54, 25, 14);
    }

    .Formulario h1{
        color: rgb(54, 25, 14);
    }

    .Formulario input {
        width: 45rem;
        height: 2.3rem;
        display: block;
        margin-top: 20px;
        padding-left: 1rem;
        border: none;
        border-radius: 5px;
        border-bottom: 3px solid #7b4b24; 
        background-color: rgba(252, 246, 238, 0.699);
    }

    .Formulario input::placeholder {
        font-size: 1rem;
        color: rgb(153, 153, 153); 
    }

    .Formulario button {
        height: 3rem;
        margin-top: 20px;
        padding: 10px 20px; 
        background-color: rgb(123, 75, 36); 
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    .Formulario button:hover {
        background-color: rgb(84, 50, 20); /* Color de fondo al pasar el mouse */
    }

    .Formulario button:disabled {
        background-color: rgb(204, 204, 204); 
        color: rgb(102, 102, 102);
        cursor: not-allowed; 
    }
    
</style>