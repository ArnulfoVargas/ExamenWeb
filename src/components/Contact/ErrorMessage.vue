<script setup>
    defineProps({
        error: Boolean,
    })
</script>

<template>
    <div :class="error ? 'showErr' : 'hideErr'">
        <p><slot></slot></p>
    </div>
</template>

<style scoped>
    div{
        display: flex;
        width: 100%;
        align-items: center;
    }

    .showErr{
        margin-top: .5rem;
        box-shadow: var(--box-shadow);
        border: var(--thin-border);
        height: 50px;
        background-color: var(--color-red);

        transition: all .2s linear;
    }

    .showErr > p {
        text-align: center;
        width: 100%;
        font-weight: bold;
        font-size: 1.5rem;
        color: white;
        font-family: var(--titles-font);

        transition: all .2s linear;
    }

    .hideErr{
        margin-top: 0;
        box-shadow: none;
        border: none;
        height: 0;
        background-color: var(--color-red);

        transition: all .2s linear;
    }

    .hideErr > p{
        text-align: center;
        width: 100%;
        font-weight: bold;
        font-size: 0;
        color: white;
        font-family: var(--titles-font);

        transition: all .2s linear;
    }
</style>