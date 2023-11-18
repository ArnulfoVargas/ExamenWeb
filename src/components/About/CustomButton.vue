<script setup>
    defineProps({
        url: {
            type: String,
            required: true
        }
    })
</script>

<template>
    <a :href="url" target="_blank">
        <div>
            <slot></slot>
        </div>
    </a>
</template>

<style scoped>
    a{
        margin: auto;
        text-decoration: none;
        color: var(--color-red);
        background-color: var(--color-white);
        border: solid var(--color-red) .25rem;
        font-family: var(--main-font);
        font-weight: bold;
        font-size: 2rem;
        cursor: pointer;
        margin-bottom: 1rem;
        box-shadow: 0;

        transition-property: background-color, border, color, box-shadow;
        transition-duration: 125ms;
        transition-timing-function: linear;
    }

    a:hover{
        color: var(--color-white);
        background-color: var(--color-red);
        border: solid var(--color-red) .25rem;

        box-shadow: var(--box-shadow);
    }

    div{
        width: 7rem;
        height: 3rem;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>