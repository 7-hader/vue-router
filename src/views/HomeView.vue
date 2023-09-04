<script setup>
import { useCounterStore } from '@/store/counter'
import { storeToRefs } from 'pinia'

const useCounter = useCounterStore()

const { increment } = useCounter
const { count, double } = storeToRefs(useCounter)
</script>

<template>
  <h1> Home counter: 
    {{ count }}
    <!-- {{ useCounter.count }} -->
  </h1>

  <h2>Doble: 
    {{ double }}
    <!-- {{ useCounter.double }} -->
  </h2>

  <button @click="increment">
  <!-- <button @click="useCounter.increment"> -->
    Increment
  </button>

</template>


<!-- <script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <TheWelcome />
  </main>
</template> -->
