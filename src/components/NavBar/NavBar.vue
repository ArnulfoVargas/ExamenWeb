<script setup>
    import { ref } from 'vue'

    import uniqid from "uniqid"

    import NavBarButtons from './NavBarButtons.vue';
    import NavBarIcon from './NavBarIcon.vue';

    let isRecentlyMounted = true;
    const isOpen = ref(false);

    const routes = [
        {to: "/", text:"Home"},
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
        isRecentlyMounted = false;
    }

    const hideHamburguer = () => {
        isOpen.value = false;
        setOverflow(false);
        isRecentlyMounted = false;
    }

    window.addEventListener('resize', () => {
        isOpen.value = false;
        setOverflow(false);
    })

</script>

<template>
    <div class="nav-bar">
        <NavBarIcon/>
        
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
            v-show="!isRecentlyMounted"
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
        width: 100%;
        height: 100%;

        position: fixed;
        top: 0;

        display: flex;
        flex-direction: column;
        justify-content: center;

        background-color: var(--color-gray);
        transition: all .25s linear;
    }

    .toggle-hide{
        animation-name: hide;
        animation-duration: .25s;
        animation-fill-mode: forwards;
    }

    .toggle-show{
        animation-name: show;
        animation-duration: .25s;
        animation-fill-mode: forwards;
    }

    @keyframes show {
        from{
            left: -100dvw;
            pointer-events: none;
        }
        to{
            left: 0;
            pointer-events: all;
        }
    }
    @keyframes hide {
        from{
            left: 0;
            pointer-events: none;
        }
        to{
            left: -100dvw;
            display: none;
        }
    }

    .toggle-show *{
        animation-name: showChild;
        animation-duration: 1.25s;
        animation-fill-mode: forwards;
    }

    @keyframes showChild {
        from{
            opacity: 0;
        }
        to{
            opacity: 1;
        }
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