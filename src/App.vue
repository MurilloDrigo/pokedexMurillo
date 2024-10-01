<script setup lang="ts">
import {ref} from 'vue'

let num = ref(0)

</script>

<template>
<!-- NavBar Bootstrap Begin-->
<nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <router-link to="/" class="navbar">
    <img src="./assets/icon.svg" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">  
    </router-link>
    
    <router-link class="navbar-brand" to="/">
      PokeVite
    </router-link>

    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <router-link class="nav-link" aria-current="page" to="#">Home</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" to="#">About</router-link>
        </li>
       
      </ul>
    </div>
  </div>
</nav>
<!-- NavBar Bootstrap End-->

 <!-- Content Begin -->
  <div class="">
    <router-view> </router-view>
  </div>

  <footer class="bg-primary text-light">
    <div> Feito em {{ new Date().getFullYear() }}</div>
  </footer>
</template>

<style scoped>
footer{
  position: fixed;
  bottom: 0;
  width: 100%;
}
</style>
