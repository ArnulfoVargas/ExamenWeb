<script setup>
    import {ref} from 'vue'

    import uniqid from "uniqid"

    import NavBarButtons from './NavBarButtons.vue';

    const isOpen = ref(false);

    const routes = [
        {to: "/home", text:"Home"},
        {to: "/about", text:"About"},
        {to: "/pokeapi", text:"PokeAPI"},
        {to: "/contact", text: "Contact"}
    ]

    const setOverflow = (overflow) => {
        document.body.className = `${overflow ? 'toggled' : ''}`;
    }

    const toggleHamburguer = () => {
        isOpen.value = !isOpen.value;
        setOverflow(isOpen.value);
    }

    const hideHamburguer = () => {
        isOpen.value = false;
        setOverflow(false);
    }

    window.addEventListener('resize', () => {
        isOpen.value = false;
        setOverflow(true);
    })
</script>

<template>
    <div class="nav-bar">
        <div class="company">
            <p>Hola</p>
        </div>
        <div class="routes">

            <NavBarButtons 
            v-for="route in routes"
            :key="uniqid()"
            :to="route.to"
            >{{ route.text }}</NavBarButtons>
        </div>
        
        <div 
            class="hamburguer"
            @click="toggleHamburguer"
            >
            <p> {{ isOpen ? '&#10006;' : '&#9776;' }}</p>
        </div>

        <div 
            class="nav-toggle"
            :class="isOpen ? 'toggle-show' : 'toggle-hide'"
            >
            <NavBarButtons 
            v-for="route in routes"
            :key="uniqid()"
            :to="route.to"
            @on-hide="hideHamburguer"
            >{{ route.text }}</NavBarButtons>
        </div>
    </div>
</template>

<style scoped>
    .nav-bar{
        position: sticky;
        top: 0;
        height: 5rem;
        width: 100%;
        background-color: var(--color-gray);
        display: flex;
        justify-content: space-between;
        z-index: 1;
    }

    .company{
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100px;
        z-index: 1;
    }

    .company p{
        margin: 0;
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        font-size: 2rem;
        color: var(--text-white);
    }
    .routes{
        display: none;
        z-index: 1;
    }

    .hamburguer{
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        width: 5rem;
        z-index: 1;
    }

    .hamburguer p{
        margin: 0;
        text-align: center;
        font-weight: bold;
        font-size: 2rem;
        color: var(--color-white);
    }
    .nav-toggle{
        width: 100dvw;
        height: 100dvh;

        position: absolute;
        top: 0;

        display: flex;
        flex-direction: column;
        justify-content: center;

        background-color: var(--color-gray);
        transition: all .25s linear;
    }

    .toggle-hide{
        left: -100dvw;
        pointer-events: none;
    }

    .toggle-show{
        left: 0;
        pointer-events: all;
        
    }

    @media (min-width: 768px){
        .routes{
            display: flex;
        }

        .hamburguer{
            display: none;
        }
    }
</style>