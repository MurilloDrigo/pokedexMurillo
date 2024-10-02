<script setup>
const pokemon = defineProps(["name","xp","height","img", "loading", "hp", "attack", "defense", "specialAttack", "specialDefense","speed","id", "type"])
</script>

<template>
    <div class="card cardPokemonSelected" :class="loading? '' : 'animate__animated animate__flipInY'">

        <img :src="pokemon.img" :alt="pokemon.name" height="250">
        <div class="card-body">
            <h5 class="card-tittle text-center ">
                {{ pokemon.name}}
                
            </h5>
            <hr>

            <div class="row">
                <section class="col">
                    <strong>HP: </strong>
                    <span>{{pokemon.hp}}</span>
                </section>
                <section class="col">
                    <strong>XP: </strong>
                    <span>{{ pokemon.xp }}</span>
                </section>
                
            </div>
            <div class="row">
                <section class="col">
                    <strong>Altura: </strong>
                    <span>{{pokemon.height}} cm</span>
                </section>
                <section class="col">
                    <strong>Attack: </strong>
                    <span>{{ pokemon.xp }}</span>
                </section>
            </div>
            <div class="row">
                
                <section class="col">
                    <strong>Defense: </strong>
                    <span>{{pokemon.height}}</span>
                </section>
                <section class="col">
                    <strong>Speed: </strong>
                    <span>{{pokemon.speed}}</span>
                </section>
            </div>
            <div class="row">
                
                <section class="col">
                    <strong>Special Defense: </strong>
                    <span>{{pokemon.specialDefense}}</span>
                </section>
                <section class="col">
                    <strong>SpecialAttack: </strong>
                    <span>{{pokemon.specialAttack}}</span>
                </section>
            </div>
            <div class="row">

                <section class="col">
                    <strong>Número: </strong>
                    <span>{{pokemon.id}}</span>
                </section>
                <section class="col">
                    <strong>Tipo: </strong>
                    <span>{{pokemon.type}}</span>
                </section>
                
            </div>
            
        </div>
    </div>
</template>

<style scoped>
.cardPokemonSelected{
    background: rgb(34,195,193);
    background: linear-gradient(0deg, rgba(34,195,193,1) 0%, rgba(40,141,207,1) 52%, rgba(45,98,253,1) 100%);
    height: 39rem;
    padding: 2rem;
    z-index: 1;
}

.cardPokemonSelected img:hover{
    padding: .2rem;
}
</style>