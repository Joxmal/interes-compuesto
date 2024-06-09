<script setup lang="ts">
import { ref } from 'vue'
const dias = ref()
const monto = ref()

import InteresCompuesto from './components/InteresCompuesto.vue';
</script>

<template>
<main class="bg-blue-300 min-h-screen h-full flex flex-col items-center justify-center bg-gradient-to-r from-blue-500 to-purple-500">
  <div>
    <input type="number" v-model="dias" placeholder="Dias" class="border border-gray-300 rounded-md p-2 m-2">
    <input type="number" v-model="monto" placeholder="Monto" class="border border-gray-300 rounded-md p-2 m-2">
  </div>
  
  
  <div v-if=" dias > 0 && monto > 0">
    <InteresCompuesto :dias=dias :monto=monto />  <!-- Agrega el componente InteresCompuesto aquĆ­ -->
  </div>
</main>

</template>

