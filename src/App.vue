<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <footer> 
    <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/cartomante">Cartomante</RouterLink>
        <RouterLink to="/Search">Search Advice</RouterLink>
      </nav>
  </footer>

  <RouterView />
</template>

<style scoped>
/* header {
  line-height: 1.5;
  max-height: 100vh;
} */


/* nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a:first-of-type {
  border: 0;
} */

/* @media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }


  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  } */

</style>
