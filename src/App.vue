<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <footer> 
    <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/cartomante">Cartomante</RouterLink>
        <RouterLink to="/search">Search Advice</RouterLink>
      </nav>
  </footer>

  <RouterView />
</template>


