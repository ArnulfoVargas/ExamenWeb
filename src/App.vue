<script setup>
import NavBar from './components/NavBar.vue';
import AppFooter from './components/AppFooter.vue'
</script>

<template>
  <NavBar/>

  <RouterView />

  <AppFooter/>
</template>
 
<style>
  @import url('https://fonts.googleapis.com/css2?family=Fragment+Mono&family=Geologica:wght@400;700&display=swap');

  :root{
    --color-gray: rgb(57, 52, 52);
    --color-dark-gray: rgb(35, 30, 30);
    --color-white: #ffffff;
    --color-red: rgb(185 28 28);

    --box-shadow: 4px 4px rgb(57, 52, 52);

    --main-font: 'Fragment Mono', monospace;
    --titles-font: 'Geologica', sans-serif;
  }

  a{
    text-decoration: none;
  }

  input[type="number"]::-webkit-inner-spin-button,
  input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  body{
    margin: 0;
  }

  *{
    user-select: none;
  }

  .toggled{
    overflow: hidden;
  }
</style>
