<script setup>
    defineProps({
        tech: {
            type: String,
            required: true
        },
        docs: String
    })
</script>

<template>
    <a :href="docs" target="_blank">
        <div>
            <img :src="tech" alt="Tech logo">
            <p><slot></slot></p>
        </div>
    </a>
</template>

<style scoped>
    a{
        color: var(--color-gray);
    }
    a:hover > div{
        transform: scale(1.25);
        cursor: pointer;
        transition: transform .2s linear;
        transition: transform .2s cubic-bezier(0, 0.65, 0.33, 1.99);
    }
    div{
        height: 9rem;
        width: 6rem;
        display: grid;
        gap: 1.75rem;
        justify-content: center;
        grid-template-rows: 4.83rem 2.41rem;
        margin-bottom: 1.5rem;

        transition: transform .2s linear;
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