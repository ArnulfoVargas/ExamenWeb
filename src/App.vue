<script setup>
import NavBar from './components/NavBar/NavBar.vue';
import AppFooter from './components/Footer/AppFooter.vue'
</script>

<template>
  <NavBar/>

  <div class="router-view">
    <RouterView />
  </div>

  <AppFooter/>
</template>
 
<style>
  @import url('https://fonts.googleapis.com/css2?family=Fragment+Mono&family=Geologica:wght@400;700&display=swap');

  :root{
    --color-gray: rgb(57, 52, 52);
    --color-dark-gray: rgb(35, 30, 30);
    --color-white: #ffffff;
    --color-red: rgb(185 28 28);
    --color-light-red: rgb(220, 38, 38);

    --text-shadow: 4px -4px rgb(57, 52, 52);
    --box-shadow: 4px 4px rgb(57, 52, 52);
    --thin-border: solid 2px rgb(57, 52, 52);

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

  .body{
    margin: auto;
    padding: 1.25rem 0;
  }

  .router-view{
    min-height: calc(100dvh - 5rem - 387px);
  }

  @media (min-width: 768px) {
    .router-view{
      min-height: calc(100dvh - 5rem - 304px);
    }
  }

  *{
    user-select: none;
    font-family: var(--main-font);
  }

  .toggled{
    overflow: hidden;
  }
</style>
