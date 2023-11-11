<script setup>
    
</script>

<template>
    <div>
        <h2><slot></slot></h2>
    </div>
</template>

<style scoped>
    div{
        margin: auto;
        width: fit-content;
        max-width: fit-content;
        padding: 0 .25rem ;
        background-color: var(--color-red);
        box-shadow: var(--box-shadow);
        border: var(--thin-border);
        display: flex;
        align-items: center;
    }
    h2{
        color: var(--color-white);
        font-size: 1.875rem;
        line-height: 1.875rem;
        margin: 0;
        text-align: center;
        font-weight: 700;
    }

    @media (min-width: 758px){
        div{
            margin: 1rem auto;
            height: 2.25rem;
        }
        h2{
            font-size: 2.25rem;
            line-height: 2.25rem;
            text-overflow: ellipsis;
        }
    }
</style>