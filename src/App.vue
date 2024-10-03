<script setup lang="ts">
import {ref} from 'vue'

let num = ref(0)

</script>

<template>
<!-- NavBar Bootstrap Begin-->
<nav class="navbar navbar-expand-lg navbar-dark bg-black bg-gradient">
  <div class="container-fluid">
    <router-link to="/" class="navbar">
    <img src="./assets/pokemon-icon.png" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">  
    </router-link>
    
    <router-link class="navbar-brand" to="/">
      Pokedex
    </router-link>

    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
     
    </div>
  </div>
</nav>
<!-- NavBar Bootstrap End-->

 <!-- Content Begin -->
  <div>
    <router-view> </router-view>
  </div>

  <footer class="bg-black bg-gradient text-light">
    <div class="d-flex w-100% bg-black justify-content-center gap-3">
      <a href="https://www.linkedin.com/in/murillo-drigo/" target="_blank" class="nav-link">Murillo Nunes Drigo </a> 
      <span> (13)991659433</span>
    </div>
  </footer>
</template>

<style scoped>
footer{
  width: 100%;
  bottom: 0;
  position: fixed;
  text-align: center;
}
</style>
