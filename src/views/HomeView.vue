<script setup lang="ts">
import CardPokemonSelected from "@/components/CardPokemonSelected.vue";
import ListPokemons from "@/components/ListPokemons.vue";
import { onMounted, reactive, ref, computed } from "vue";


let pokemons = reactive(ref());
let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")
let searchPokemonField = ref("")
let pokemonSelected = reactive(ref())
let loading = ref(false)

onMounted(()=>{
  fetch("https://pokeapi.co/api/v2/pokemon/?limit=200&offset=0")
  .then(res => res.json())
  .then(res => pokemons.value = res.results);
})

const pokemonsFiltered = computed(()=>{
  if(pokemons.value && searchPokemonField.value){


    return pokemons.value.filter((pokemon: { name: string; }) =>
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    )
  }
  return pokemons.value;
})

const selectedPokemon = async (pokemon: any) => {
  loading.value = true;
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => pokemonSelected.value = res)
  .catch(err => alert(err))
  .finally(() => {
    loading.value = false;
  })
}

</script>

<template>
<div class="container mt-5">
  <div class="row mt-4">
  <div class="col-sm-6 col-md-6 z-1">

  <CardPokemonSelected
  :name="pokemonSelected?.name"
  :xp="pokemonSelected?.base_experience"
  :height="pokemonSelected?.height"
  :img="pokemonSelected?.sprites.other.dream_world.front_default"
  :loading="loading"
  />
  </div>
    <div class="col-sm-6 col-md-6 z-3">
      <!-- divisor que separa em linhas  -->
      <div class="input-group mb-3 ">
        <label hidden class="input-group-text" id="seachPokemonField">Pesquisar</label>
        <input v-model="searchPokemonField" type="text" class="form-control" id="seachPokemonField" placeholder="Pesquisar Pokemon...">
      </div>
       <div class="card card-list">
         <div class="card-body row">
      
           
           
           <ListPokemons
           v-for="pokemon in pokemonsFiltered"
           :key="pokemon.name"
           :name="pokemon.name"
           :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6]+'.svg'"
           @click="selectedPokemon(pokemon)"
           />

       </div>
      </div>
      
    </div>
    
  </div>
</div>
  
  
</template>

<style scoped>
.card-list{
  overflow-y: scroll;
  overflow-x: hidden;
  height: 35rem;
  z-index: 20;
}

</style>
