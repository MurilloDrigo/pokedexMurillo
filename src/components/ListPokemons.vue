<script setup>
const pokemon = defineProps(["name", "num", "urlBaseSvg"])
</script>

<template> 
    
        <div class="col-4">

            <div class="card p-2 mb-3 cardListPokemon">
                <p class="text-center">{{ pokemon.name }}</p>
                <img :src="urlBaseSvg" class="card-img-top" alt="pokemon image" height="140"/> 
                <p class="text-center">Nº {{ pokemon.num }}</p>
            </div>
        </div>
    
</template>

<style scoped>
.cardListPokemon{
    
    cursor: pointer;
    background: rgb(223,223,223);
    background: radial-gradient(circle, rgba(223,223,223,1) 7%, rgba(100,196,218,1) 36%, rgba(2,87,103,1) 100%);
}
.cardListPokemon:hover{
    background: rgb(255,255,255);
    background: radial-gradient(circle, rgba(255,255,255,1) 7%, rgba(145,234,255,1) 36%, rgba(1,138,164,1) 100%);
    cursor: pointer;
}
.cardListPokemon img:hover{
    padding: .2rem;
}
</style>