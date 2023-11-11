<script setup>
    import { RouterLink } from 'vue-router';
</script>

<template>
    <RouterLink to="/">
        <div class="company">
            <div class="circle"></div>
            <img src="../assets/Logo.png" alt="Logo image">
        </div>
    </RouterLink>
</template>

<style scoped>
  .company{
        position: relative;
        height: 5rem;
        width: 5rem;
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 1;
        margin-left: 1.5rem;
    }

    .circle{
        background-color: var(--color-red);
        height: 80%;
        width: 80%;
        border-radius: 50%;
    }

    .company p{
        margin: 0;
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        font-size: 2rem;
        color: var(--text-white);
    }

    .company img{
        position: absolute;
        height: 70%;
        width: 70%;
    }
</style>