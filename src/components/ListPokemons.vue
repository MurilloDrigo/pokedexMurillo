<script setup lang="ts">
import { defineProps } from 'vue';

// Definindo as propriedades esperadas no componente
const props = defineProps<{
  name: string;
  num: string;
  urlBaseSvg: string;
}>();
</script>

<template>
  <div class="col">
    <div class="card p-2 cardListPokemon text-capitalize">
      <p class="text-center">{{ name }}</p>
      <img :src="urlBaseSvg" class="card-img-top" alt="pokemon image" height="140"/>
      <p class="text-center">Nº {{ num }}</p>
    </div>
  </div>
</template>

<style scoped>
.cardListPokemon {
  cursor: pointer;
  background: rgb(223, 223, 223);
  background: radial-gradient('linear-gradient(135deg, #a7a7a7, #ffffff)');
}
.cardListPokemon:hover {
  background: rgb(255, 255, 255);
  background: radial-gradient(circle, rgba(255, 255, 255, 1) 7%, rgba(145, 234, 255, 1) 36%, rgba(1, 138, 164, 1) 100%);
  cursor: pointer;
}
.cardListPokemon img:hover {
  padding: 0.2rem;
}
</style>
