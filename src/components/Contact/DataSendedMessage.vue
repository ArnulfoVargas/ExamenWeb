<script setup>
    defineProps({
        sended: Boolean,
    })
</script>

<template>
    <div :class="sended ? 'showSend' : 'hideSend'">
        <p>Sended Succesfully</p>
    </div>
</template>

<style scoped>
    div{
        display: flex;
        width: 100%;
        align-items: center;
    }

    .showSend{
        margin-bottom: 1rem;
        box-shadow: var(--box-shadow);
        border: var(--thin-border);
        height: 50px;
        background-color: rgb(19, 167, 19);

        transition: all .2s linear;
    }

    .showSend > p {
        text-align: center;
        width: 100%;
        font-weight: bold;
        font-size: 1.5rem;
        color: white;
        font-family: var(--titles-font);

        transition: all .2s linear;
    }

    .hideSend{
        margin-top: 0;
        box-shadow: none;
        border: none;
        height: 0;
        background-color: rgb(19, 167, 19);

        transition: all .2s linear;
    }

    .hideSend > p{
        text-align: center;
        width: 100%;
        font-weight: bold;
        font-size: 0;
        color: white;
        font-family: var(--titles-font);

        transition: all .2s linear;
    }
</style>