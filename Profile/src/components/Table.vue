<template>
    <div class="Contenedor">
        <table>
            <thead>
                <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>Correo</th>
                <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="user in Usuarios" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
                <td>{{ user.lastname }}</td>
                <td>{{ user.email }}</td>
                <td class="acciones">
                    <button class="editar">Editar</button>
                    <button class="eliminar">Eliminar</button>
                </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup lang="ts">
    import type { IUser } from './Interfaces/InterUsuarios';
    import ObjectUser from './Data/DataUsuarios'

    import {ref} from 'vue'

    const Usuarios = ref<IUser[]>(ObjectUser);

</script>

<style scoped>
    .Contenedor{
        display: flex;
        justify-content: center;
    }

    table {
        width: 50%;
        border-collapse: collapse;
        margin-top: 3rem;
        background-color: rgba(247, 245, 238, 0.863);
        border: 8px solid rgb(54, 25, 14); 
    }

    th, td {
        padding: 10px;
        border-bottom: 2px solid rgb(54, 25, 14); 
        color: rgb(0,0,0);
    }

    th {
        background-color: rgb(123, 75, 36); 
    }

    tr:nth-child(even) {
        background-color: rgba(252, 246, 238, 0.699); 
    }

    tr:hover {
        background-color: rgb(233, 223, 206); 
    }

    .acciones {
        display: flex;
        justify-content: space-around;
    }

    .editar, .eliminar {
        padding: 5px 10px;
        background-color: rgb(123, 75, 36);
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    .editar:hover, .eliminar:hover {
        background-color: rgb(84, 50, 20); 
    }

</style>