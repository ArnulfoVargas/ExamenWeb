<script setup>
    defineProps({
        tech: {
            type: String,
            required: true
        },
    })
</script>

<template>
    <div>
        <img :src="tech" alt="Tech logo">
        <p><slot></slot></p>
    </div>
</template>

<style scoped>
    div{
        height: 9rem;
        width: 6rem;
        display: grid;
        gap: 1.75rem;
        justify-content: center;
        grid-template-rows: 4.83rem 2.41rem;
        margin-bottom: 1.5rem;
    }
    p{
        text-align: center;
        margin: 0;
    }
    img{
        height: 4.83rem;
        width: 4.83rem;
        margin: auto;
    }
</style>