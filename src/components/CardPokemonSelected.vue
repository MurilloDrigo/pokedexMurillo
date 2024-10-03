<script setup>
import { computed } from 'vue';

const pokemon = defineProps(["name", "xp", "height", "img", "loading", "hp", "attack", "defense", "specialAttack", "specialDefense", "speed", "id", "type"]);

// Computed para determinar o gradiente de fundo com base no tipo do Pokémon
const backgroundColor = computed(() => {
    switch (pokemon.type.toLowerCase()) {
        case 'grass':
            return 'linear-gradient(135deg, #56ab2f, #a8e063)'; 
        case 'bug':
            return 'linear-gradient(135deg, #c1ff75, #d1dab2)'; 
        case 'poison':
            return 'linear-gradient(135deg, #a83eff, #eedaff)'; 
        case 'fire':
            return 'linear-gradient(135deg, #ff4b2b, #ffb410)';
        case 'fighting':
            return 'linear-gradient(135deg, #ff416c, #ff4b2b)'; 
        case 'water':
            return 'linear-gradient(135deg, #36d1dc, #5b86e5)';
        case 'electric':
            return 'linear-gradient(135deg, #ffd200, #ffd7aa)'; 
        case 'psychic':
            return 'linear-gradient(135deg, #a18cd1, #fbc2eb)';
        case 'rock':
            return 'linear-gradient(135deg, #3b386e, #393939)'; 
        case 'ice':
            return 'linear-gradient(135deg, #74ebd5, #acb6e5)'; 
        case 'dragon':
            return 'linear-gradient(135deg, #beaaff, #aac7ff)';
        case 'ground':
            return 'linear-gradient(135deg, #ba8b02, #181818)';
        case 'ghost':
            return 'linear-gradient(135deg, #84679c, #2b1240)';
        case 'fairy':
            return 'linear-gradient(135deg, #ebd4ff, #ff13e6)';
        case 'steel':
            return 'linear-gradient(135deg, #d7d5ff, #3c3b49)';
        case 'flying':
            return 'linear-gradient(135deg, #dce494, #6bb9b7)';
        case 'dark':
            return 'linear-gradient(135deg, #030038, #000000)';
        default:
            return 'linear-gradient(135deg, #fbffee, #625454)';
    }
});
</script>
<template>
    <div class="d-flex justify-content-center flex-wrap mt-4 gap-3">
      <div
        class="card overflow-hidden p-2" 
        :class="loading ? '' : 'animate__animated animate__flipInY '"
        :style="{ background: backgroundColor, width: '23rem' }">
        <div class="d-flex justify-content-between card-title p-2 bg-light bg-gradient rounded-top text-capitalize m-0">

            <h5>
              {{ pokemon.name }}
            </h5>
            <h5>
                Nº: 
                {{ pokemon.id }}
            </h5>
        </div>
        
        <img class="border border-5 border-light p-3" :src="pokemon.img" :alt="pokemon.name" style="height: 300px; object-fit: contain;"> 
        <div class="card-body bg-light bg-gradient">
          <hr>
          <div class="row">
            <section class="col">
              <strong>HP: </strong>
              <span>{{ pokemon.hp }}</span>
            </section>
            <section class="col">
              <strong>XP: </strong>
              <span>{{ pokemon.xp }}</span>
            </section>
          </div>
          <div class="row">
            <section class="col">
              <strong>Altura: </strong>
              <span>{{ pokemon.height * 10 }} cm</span>
            </section>
            <section class="col">
              <strong>Attack: </strong>
              <span>{{ pokemon.attack }}</span>
            </section>
          </div>
          <div class="row">
            <section class="col">
              <strong>Defense: </strong>
              <span>{{ pokemon.defense }}</span>
            </section>
            <section class="col">
              <strong>Speed: </strong>
              <span>{{ pokemon.speed }}</span>
            </section>
          </div>
          <div class="row">
            <section class="col">
              <strong>Special-Defense: </strong>
              <span>{{ pokemon.specialDefense }}</span>
            </section>
            <section class="col">
              <strong>Special-Attack: </strong>
              <span>{{ pokemon.specialAttack }}</span>
            </section>
          </div>
          <div class="row">
            <section class="col text-capitalize">
                <strong>Tipo: </strong>
                <span>{{ pokemon.type }}</span>
            </section>
            <section class="col">
              
            </section>
          </div>
        </div>
      </div>
    </div>
  </template>
  

<style scoped>



</style>
