<script setup>
    defineProps({
        data : {
            type: Object,
            required: true,
        }
    })
</script>

<template>
    <a :href="data.link">
        <div class="card">
            <img :src="data.image" alt="Logo " :alt="data.name">
            <p>{{ data.name }}</p>
        </div>
    </a>
</template>

<style scoped>
    .card{
        display: grid;
        grid-template-rows: 5rem auto;
    }

    .card img{
        height: 100%;
        width: 100%;
        opacity: .5;
    }
    .card p, .card p:active, .card p:hover{
        margin: 0;
        text-align: center;
        color: black;
        opacity: .5;
        margin-top: .5rem;
    }
</style>