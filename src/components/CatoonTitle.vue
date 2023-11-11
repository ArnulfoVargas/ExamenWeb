<template>
    <div>
        <h1><slot></slot></h1>
    </div>
</template>

<style scoped>
    div{
        margin: auto;
        width: fit-content;
        height: fit-content;
        padding: 0 .25rem ;
        background-color: var(--color-red);
        box-shadow: var(--box-shadow);
        border: var(--thin-border);
        display: flex;
        align-items: center;
    }
    h1{
        color: var(--color-white);
        font-family: var(--titles-font);
        font-size: 3rem;
        line-height: 3rem;
        margin: 0;
        text-align: center;
        font-weight: bold;
        text-shadow: var(--text-shadow);
    }

    @media (min-width: 758px){
        div{
            margin: 1rem auto;
            height: 4.5rem;
        }
        h1{
            font-size: 4.5rem;
            line-height: 4.5rem;
        }
    }
</style>