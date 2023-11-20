<script setup>
    import { ref, onMounted, computed } from 'vue';

    const props = defineProps({
        shinyImage: String,
        normalImage: String,
    })

    const isShiny = ref(false)

    onMounted(() => {
        const holder = localStorage.getItem("shiny")

        if(holder == null || holder == undefined){
            isShiny.value = false;
            return;
        }

        isShiny.value = holder === "s" ? true : false;
    })

    const onShiny = () => {
        isShiny.value = !isShiny.value;
        localStorage.setItem("shiny", isShiny.value ? "s" : "n")
    }

    const getImage = computed(() => {
        return isShiny.value ? props.shinyImage : props.normalImage
    })
</script>

<template>
    <div>
        <img :src="getImage" alt="">
        <button @click="onShiny">{{ isShiny ? "Normal" : "Shiny" }}</button>
    </div>
</template>

<style scoped>
    div{
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1rem;
    }

    img{
        width: 24rem;
        filter: drop-shadow(var(--box-shadow));
    }

    button{
        background-color: var(--color-white);
        color: var(--color-red);
        border: none;
        font-family: var(--main-font);
        border: solid var(--color-red) .25rem;
        font-weight: bold;
        cursor: pointer;
        border-radius: 0;
        font-size: 2rem;
        padding: .25rem .5rem;
        
        transition-property: background-color, border, color, box-shadow;
        transition-duration: 125ms;
        transition-timing-function: linear;
    }

    button:hover{
        color: var(--color-white);
        background-color: var(--color-red);
        border: solid var(--color-red) .25rem;

        box-shadow: var(--box-shadow);
    }
</style>