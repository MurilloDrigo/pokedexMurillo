  <script setup lang="ts">
  import CardPokemonSelected from "@/components/CardPokemonSelected.vue";
  import ListPokemons from "@/components/ListPokemons.vue";
import PokemonEvolutions from "@/components/PokemonEvolutions.vue";
  import { onMounted, reactive, ref, computed } from "vue";

  // Interface para definir o tipo de Pokémon
  interface Pokemon {
    name: string;
    url: string;
  }

  interface PokemonDetail {
    name: string;
    id: number;
    base_experience: number;
    height: number;
    sprites: {
      other: {
        dream_world: {
          front_default: string;
        };
      };
    };
    stats: { base_stat: number }[];
    types: { type: { name: string } }[];
  }

  interface PokemonDetails {
  name: string;
  types: { type: { name: string } }[];
}


  // Definição de estados reativos
  const pokemons = ref<Pokemon[]>([]);  // Especificando o tipo correto
  const urlBaseSvg = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/";
  const searchPokemonField = ref("");
  const pokemonSelected = ref<PokemonDetail | null>(null);  // Definindo o tipo detalhado do Pokémon
  const loading = ref(false);

  //Busca Por Tipo


  // Função para buscar os Pokémons na API
  const fetchPokemons = async () => {
    try {
      const response = await fetch("https://pokeapi.co/api/v2/pokemon/?offset=0&limit=649");
      const data = await response.json();
      pokemons.value = data.results;
    } catch (error) {
      console.error("Erro ao buscar Pokémons:", error);
    }
  };

  // Função que é executada assim que o componente é montado
  onMounted(fetchPokemons);

  // Computed para filtrar os Pokémons
  const pokemonsFiltered = computed(() => {
    const searchValue = searchPokemonField.value.trim().toLowerCase();
    
    if (!searchValue) return pokemons.value;

    return pokemons.value.filter(pokemon => {
      const id = pokemon.url.split('/')[6];
      
      if (!isNaN(Number(searchValue))) {
        return id === searchValue;
      }
      
      return pokemon.name.toLowerCase().includes(searchValue);
    });
  });

  // Função para buscar dados detalhados de um Pokémon selecionado e ir até a carta
  const selectedPokemon = async (pokemon: Pokemon) => {
    loading.value = true;
    try {
      const response = await fetch(pokemon.url);
      const data = await response.json();
      pokemonSelected.value = data;
    } catch (error) {
      console.error("Erro ao selecionar Pokémon:", error);
    } finally {
      loading.value = false;
      const cardElement = document.getElementById("cardRef");
      if (cardElement) {
        cardElement.scrollIntoView({ behavior: 'smooth' });
      }
  
    }
  };

  
  </script>


  <template >
        <div class="d-flex justify-content-center align-items-center flex-wrap gap-4 p-3 container">
          <!-- Input e lista -->
          <div class="flex-column col">
            <div class="input-group mb-3 ">
              <input
              v-model="searchPokemonField"
              type="text"
              class="form-control"
              placeholder="Pesquisar Pokémon..."
              />
            </div>
            <div class="card card-list bg-dark bg-gradient ">
              <div class="d-flex justify-content-center flex-wrap">
                <ListPokemons
                class="card-body"
                v-for="pokemon in pokemonsFiltered"
                :key="pokemon.url"
                :num="pokemon.url.split('/')[6]"
                :name="pokemon.name"
                :urlBaseSvg="`${urlBaseSvg}${pokemon.url.split('/')[6]}.svg`"
                @click="selectedPokemon(pokemon)"
                />
              </div>
            </div>
          </div>
          <!-- Cartão -->
          <div class="col" id="cardRef">
            <CardPokemonSelected
              v-if="pokemonSelected"
              :name="pokemonSelected.name"
              :id="pokemonSelected.id"
              :xp="pokemonSelected.base_experience"
              :height="pokemonSelected.height"
              :img="pokemonSelected.sprites.other.dream_world.front_default"
              :hp="pokemonSelected.stats[0].base_stat"
              :attack="pokemonSelected.stats[1].base_stat"
              :defense="pokemonSelected.stats[2].base_stat"
              :specialAttack="pokemonSelected.stats[3].base_stat"
              :specialDefense="pokemonSelected.stats[4].base_stat"
              :speed="pokemonSelected.stats[5].base_stat"
              :type="pokemonSelected.types[0].type.name"
              :loading="loading"
            />
          </div>
        </div>
      <PokemonEvolutions v-if="pokemonSelected" :id="pokemonSelected.id" />
    
  </template>

  <style scoped>
  .card-list {
    overflow-y: auto;
    height: 35rem;
  }

  
  </style>
