<script setup lang="ts">
import { defineProps, ref, watch } from "vue";

// Recebe a prop `id` do Pokémon selecionado
const props = defineProps<{ id: number }>();
const evolutions = ref<any[]>([]);
const showEvolutions = ref(false);

// URL base para as imagens dos Pokémon
const imageUrlBase = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/";

const fetchEvolutions = async () => {
  try {
    // Limpa as evoluções anteriores
    evolutions.value = [];
    showEvolutions.value = false;

    // Buscar a espécie do Pokémon, que contém a URL da cadeia de evolução
    const speciesResponse = await fetch(`https://pokeapi.co/api/v2/pokemon-species/${props.id}/`);
    
    if (!speciesResponse.ok) {
      throw new Error(`Erro ao buscar dados da espécie: ${speciesResponse.statusText}`);
    }

    const speciesData = await speciesResponse.json();
    const evolutionChainUrl = speciesData.evolution_chain.url;

    // Buscar a cadeia de evolução
    const evolutionResponse = await fetch(evolutionChainUrl);

    if (!evolutionResponse.ok) {
      throw new Error(`Erro ao buscar a cadeia de evolução: ${evolutionResponse.statusText}`);
    }

    const evolutionData = await evolutionResponse.json();

    // Função recursiva para extrair todas as evoluções com nome, nível mínimo, trigger e ID da espécie
    const extractEvolutions = async (chain: any, evoArray: any[] = []) => {
      const speciesId = chain.species.url.split("/").slice(-2, -1)[0]; // Extrair o ID da espécie da URL

      evoArray.push({
        species_name: chain.species.name,
        min_level: chain.evolution_details[0]?.min_level || null,
        trigger: chain.evolution_details[0]?.trigger?.name || null,
        imageUrl: `${imageUrlBase}${speciesId}.svg`, // Gerar a URL da imagem do Pokémon com o ID extraído
      });

      setTimeout(() => {
      showEvolutions.value = true;
    }, 10);
      if (chain.evolves_to.length > 0) {
        for (const evolution of chain.evolves_to) {
          await extractEvolutions(evolution, evoArray);
        }
      }

      return evoArray;
    };

    evolutions.value = await extractEvolutions(evolutionData.chain);

  } catch (error) {
    console.error("Erro ao buscar evoluções:", error);
  }
};

// Observa mudanças no ID e busca as evoluções novamente quando o ID mudar
watch(() => props.id, () => {
  fetchEvolutions();
});

// Inicializa o componente com as evoluções do Pokémon atual
fetchEvolutions();
</script>

<template>
  <hr class="text-white">
  <div v-if="showEvolutions">
    <div class="align-items-center" v-if="evolutions.length >= 2">
      <h5 class="text-center text-white">Evoluções</h5>
        <div class="d-flex justify-content-center flex-wrap mt-4 gap-3 ">
            <div class="card overflow-hidden p-5 bg-dark bg-gradient " v-for="evolution in evolutions" :key="evolution.species_name">
              <!-- Exibir imagem do Pokémon -->
              <img class="text-center" :src="evolution.imageUrl" :alt="evolution.species_name" height="250" />

              <h4 class="text-center text-capitalize text-white">

                  {{ evolution.species_name }} 
              </h4> 
              <!-- Exibir nome, nível mínimo e trigger -->
              <span class="card-body text-center text-white" v-if="evolution.min_level">Nível mínimo: {{ evolution.min_level }}</span>
              <span class="card-body text-center text-white" v-if="evolution.trigger">Trigger: {{ evolution.trigger }}</span>
              </div>
          
      </div>
    </div>
    <div class="text-white text-center" v-else>
      <p>Este Pokémon não possui evoluções.</p>
    </div>
</div>
</template>

<style scoped>

</style>
