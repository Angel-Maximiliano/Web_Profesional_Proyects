<script setup lang="ts">
    import CharactersData from '@/Data/CharactersContent';
    import type { Characters } from '@/Interfaces/CharactersInterface';
    import CharactersInterface from './CharactersInterface.vue';
    import CharactersForm from './CharactersForm.vue';
    
    import { ref } from 'vue'
    import type { Ref } from 'vue'
    
    const personajes = ref<Characters[]>(CharactersData)

    const name: Ref<string> = ref('')
    const lastname: Ref<string> = ref('')
    const age: Ref<number> = ref(0)
    const personality: Ref<string> = ref('')
    const occupation: Ref<string> = ref('')
    const hobby: Ref<string> = ref('')
    const pet: Ref<string> = ref('')
    const likes: Ref<string> = ref('')
    const dislikes: Ref<string> = ref('')
    const preciousobject: Ref<string> = ref('')
    const boton: Ref<boolean> = ref(true)

    const errores = ref({
        name: '',
        lastname:'',
        age: '',
        personality:'',
        occupation: '',
        hobby:'',
        pet:'',
        likes: '',
        dislikes:'',
        preciousobject:''
    })    

    const Validaciones=() =>{
        if(name.value.trim() == ''){
            errores.value.name = 'El campo nombre no puede estar vacío'
        }else if(name.value.length > 25){
            errores.value.name = 'El nombre no puede ser mayor a 25 caracteres'
        }else{
            errores.value.name=''
        }

        if(lastname.value.trim() == ''){
            errores.value.lastname = 'El campo nombre no puede estar vacío'
        }else if(lastname.value.length > 25){
            errores.value.lastname = 'El apellido no puede ser mayor a 25 caracteres'
        }else{
            errores.value.lastname=''
        }

        if(age.value <= 0){
            errores.value.age = 'La edad debe ser mayor a 0'
        }else{
            errores.value.age = ''
        }

        if(personality.value.trim() == ''){
            errores.value.personality = 'El campo nombre no puede estar vacío'
        }else{
            errores.value.personality = ''
        }

        if(occupation.value.trim() == ''){
            errores.value.occupation = 'El campo nombre no puede estar vacío'
        }else{
            errores.value.occupation = ''
        }

        if(hobby.value.trim() == ''){
            errores.value.hobby = 'El campo nombre no puede estar vacío'
        }else{
            errores.value.hobby  = ''
        }

        if(pet.value.trim() == ''){
            errores.value.pet = 'El campo nombre no puede estar vacío'
        }else{
            errores.value.pet  = ''
        }

        if(likes.value.trim() == ''){
            errores.value.likes = 'El campo nombre no puede estar vacío'
        }else{
            errores.value.likes  = ''
        }

        if(dislikes.value.trim() == ''){
            errores.value.dislikes = 'El campo nombre no puede estar vacío'
        }else{
            errores.value.dislikes  = ''
        }

        if(preciousobject.value.trim() == ''){
            errores.value.preciousobject = 'El campo nombre no puede estar vacío'
        }else{
            errores.value.preciousobject  = ''
        }

        if(errores.value.name=='' && errores.value.lastname=='' && errores.value.age == '' && errores.value.personality=='' && errores.value.occupation=='' && errores.value.hobby=='' && errores.value.pet=='' && errores.value.likes=='' && errores.value.dislikes=='' && errores.value.preciousobject==''){
            boton.value= false
        }else{
            boton.value = true
        }

    }


    const Insertado=() =>{
          // Verificacion del objeto por medio del name para validar que no haya otro almacenado de la misma manera
        if (personajes.value.some((personaje) => personaje.name === name.value) && personajes.value.some((personaje) => personaje.lastname === lastname.value)) {
            alert('Este personaje ya existe, favor de ingresar otro')
            return
        }

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
            preciousobject: preciousobject.value,
            BackColor:'',
            TextColor:''
        }

        personajes.value.push(nuevoOC)

        name.value=''
        lastname.value=''
        age.value=0
        personality.value=''
        occupation.value=''
        hobby.value=''
        pet.value=''
        likes.value=''
        dislikes.value=''
        preciousobject.value=''
    }
</script>


<template>
    <main>
        <form @submit.prevent="Insertado">
            <div :class="{ 'formulario': true }" @input="Validaciones">
                <h1>Formulario VUE</h1>
                <input type="text" v-model="name" placeholder="Nombre(s)">
                <p v-if="errores.name">{{ errores.name }}</p>
                <input type="text" v-model="lastname" placeholder="Apellidos">
                <p v-if="errores.lastname">{{ errores.lastname }}</p>
                <input type="number" v-model="age" placeholder="Edad">
                <p v-if="errores.age">{{ errores.age }}</p>
                <input type="text" v-model="personality" placeholder="Personalidad">
                <p v-if="errores.personality">{{ errores.personality }}</p>
                <input type="text" v-model="occupation" placeholder="Ocupación">
                <p v-if="errores.occupation">{{ errores.occupation }}</p>
                <input type="text" v-model="hobby" placeholder="Pasatiempo">
                <p v-if="errores.hobby">{{ errores.hobby }}</p>
                <input type="text" v-model="pet" placeholder="Mascota">
                <p v-if="errores.pet">{{ errores.pet }}</p>
                <input type="text" v-model="likes" placeholder="Le gusta">
                <p v-if="errores.likes">{{ errores.likes }}</p>
                <input type="text" v-model="dislikes" placeholder="No le gusta...">
                <p v-if="errores.dislikes">{{ errores.dislikes }}</p>
                <input type="text" v-model="preciousobject" placeholder="Objeto preciado">
                <p v-if="errores.preciousobject">{{ errores.preciousobject }}</p>
                <button class="submit" :disabled="boton">Agregar</button>
            </div>
        </form>
    </main>



    <div>
        <ul>
            <CharactersInterface
            v-for="personaje in personajes"
            :object="personaje"
            :key="personaje.id"
            />
        </ul>
    </div>  
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