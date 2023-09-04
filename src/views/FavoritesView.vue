<script setup>
import { storeToRefs } from 'pinia'
import { useFavoritesStore } from '@/store/favorites'
import { computed } from 'vue'
import { RouterLink } from 'vue-router';

const useFavorites = useFavoritesStore()
const { favorites } = storeToRefs(useFavorites)
const { remove } = useFavorites

const noFavorites = computed(() => favorites.value.length === 0)

</script>

<template>
    <h1>Favoritos</h1>
    <p v-if="noFavorites">Sin Favoritos</p>
    <ul class="list-groud ps-0"
        v-else
    >
        <li class="list-group-item d-flex justify-content-between"
            v-for="pokemon in favorites"
            :key="pokemon.id"
        >            
            <span>{{ pokemon.name }}</span>
            <div class="btn-group">
                <RouterLink :to="`/pokemons/${pokemon.name}`"
                class="btn btn-sm btn-primary"
                >
                    Detalles
                </RouterLink>
                <button 
                    class="btn btn-sm btn-danger"
                    @click="remove(pokemon.id)"
                >
                    Eliminar
                </button>
            </div>
        </li>
    </ul>
</template>