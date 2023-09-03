<script setup>
// import axios from 'axios';
// import { ref } from 'vue';
// const pokemons = ref([])
// const getData = async () => {
//     try {
//         const { data } = await axios.get('https://pokeapi.co/api/v2/pokemon')
//         pokemons.value = data.results
//     } catch (error) {
//         console.log(error)
//     }
// }
// getData()

import { RouterLink } from 'vue-router';
import { useGetData } from '@/composables/getData';

const { getData, data, error, loading } = useGetData();

getData('https://pokeapi.co/api/v2/pokemon')
</script>

<template>
    <h1>Pokemons!</h1> 
    <p v-if="loading">Cargando Pokemons...</p>   
    <p class="alert alert-danger" v-if="error">
        <strong>Error de servidor.</strong> <br> {{ error }}
    </p>
    <div v-if="data">
        <ul>
            <li v-for="(pokemon, index) in data.results"
                :key="index"
            >
                <RouterLink
                    :to="`/pokemons/${pokemon.name}`"
                >
                    {{ pokemon.name }}
                </RouterLink>
            </li>
        </ul>
        <div class="my-2">
            <button
                class="btn btn-outline-danger me-2"
                @click="getData(data.previous)"
                :disabled="!data.previous"
            >
                Previous
            </button>
            <button
                class="btn btn-outline-primary"
                @click="getData(data.next)"
                :disabled="!data.next"
            >
                Next
            </button>
        </div>
    </div>
</template>