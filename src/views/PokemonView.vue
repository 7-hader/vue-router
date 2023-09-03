<script setup>
// import axios from 'axios';
// import { ref } from 'vue';
// const pokemon = ref({})
// const getData = async () => {
//     try {
//         const { data } = await axios.get(
//             `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
//         )
//         pokemon.value = data
//     } catch (error) {
//         console.log(error)
//         pokemon.value = null
//     }
// }
// getData()

import { useRoute, useRouter } from 'vue-router'
import { useGetData } from '@/composables/getData';

const route = useRoute()
const router = useRouter()

const { getData, data:pokemon, error, loading } = useGetData();

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)

const goBack = () => {
    router.push('/pokemons')
}

</script>

<template>
    <p v-if="loading">Cargando Pokemon...</p> 
    <p class="alert alert-danger" v-if="error">
        <strong>Error de servidor.</strong> <br> {{ error }}
    </p>
    <template v-if="pokemon">
        <img :src="pokemon.sprites?.front_default" alt="">
        <h1>
            Soy un 
            {{ route.params.name }}
            <!-- {{ $route.params.name }} -->
        </h1>
    </template>    
    <!-- <h1 v-else>El Pekemon no existe!</h1> -->
    
    <button 
        class="btn btn-outline-primary"
        @click="goBack">
        Volver atrás
    </button>
</template>