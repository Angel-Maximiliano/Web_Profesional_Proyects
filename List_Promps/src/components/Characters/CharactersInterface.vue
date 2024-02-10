<template>
    <div class="card" :style="{backgroundColor: BackColor, color: TextColor}">
        <span class="left-column">
            <h3>{{ props.object.name + ' ' + props.object.lastname}}</h3>
            <button @click="Magia">Magia</button>
        </span>
        <span class="center-column">
            <div>
                <p>{{ 'Edad: ' + props.object.age }}</p>
                <p>{{ 'Pasatiempo(s): ' + props.object.personality }}</p>
                <p>{{ 'Ocupación: ' + props.object.occupation }}</p>
                <p>{{ 'Pasatiempo(s): ' + props.object.hobby }}</p>
            </div>
        </span>
        <span class="right-column">
            <div>
                <p>{{ 'Mascota(s): ' + props.object.pet }}</p>
                <p>{{ 'Gustos: ' + props.object.likes }}</p>
                <p>{{ 'Disgustos: ' + props.object.dislikes }}</p>
                <p>{{ 'Objeto preciado: ' + props.object.preciousobject }}</p>
            </div>
        </span>
    </div>
</template>

<script setup lang="ts">
    import type { Characters } from '@/Interfaces/CharactersInterface';
    import {defineProps, defineEmits} from 'vue'
    import { ref } from 'vue'
        
    const props = defineProps<{object:Characters}>();   
    const emits = defineEmits(['Magia'])

    const BackColor = ref<string>('rgba(242, 243, 235, 0.705)')
    const TextColor = ref<string>(' rgb(56, 38, 20)')

    const Magia = () => {
    const randomColor = () => Math.floor(Math.random() * 256)

    const ColorBack = `rgb(${randomColor()}, ${randomColor()}, ${randomColor()})`
    const ColorText = `rgb(${randomColor()}, ${randomColor()}, ${randomColor()})`

    // Actualizar los colores
    BackColor.value = ColorBack
    TextColor.value = ColorText
    // Emitir el evento con los colores actualizados
    emits('Magia', {
        id: props.object.id,
        BackColor: ColorBack,
        TextColor: ColorText
    })
}
</script>

<style scoped>
.card {
    width: auto;
    padding: 2rem 2rem 2rem 0rem;
    margin-top: 2rem;
    text-align: center;
    /* background-color: ; */
    border: 5px solid rgb(83, 62, 39);
    display: flex;
    justify-content: space-between;
    text-align: justify;
}

/* .card p, h3{
    color:;
} */

.left-column, .right-column, .center-column {
    flex: 1;
    margin-left: 1rem;
}

.right-column{
    padding-left: 1rem;
}

.card button{
    height: 4rem;
    width: 6rem;
    margin-top: 1rem;
    border-radius: 5px;
    color: white;
    border: 2px solid rgb(56, 38, 20);
    background-color: rgba(143, 71, 0, 0.644);
}
</style>