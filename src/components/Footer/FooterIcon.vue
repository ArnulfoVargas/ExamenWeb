<script setup>
    import { RouterLink } from "vue-router"    
</script>

<template>
    <RouterLink to="/">
        <div>
            <img src="../../assets/Logo.png" alt="Arnulfo Logo">
        </div>
    </RouterLink>
</template>

<style scoped>
    div{
        height: 6rem;
        width: 6rem;
        margin: 2rem 0;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 100%;
        background-color: var(--color-red);
    }
    img{
        width: 90%;
        height: 90%;
    }

    @media (min-width: 768px) {
        div{
            height: 10rem;
            width: 10rem;
        }
    }
</style>