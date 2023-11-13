<script setup>
    
</script>

<template>
    <div>
        <p><slot></slot></p>
    </div>
</template>

<style scoped>
    div{
        width: 75%;
        margin: 2rem auto;
    }
    p{
        font-size: 1.125rem;
        line-height: 1.75rem;
        text-align: center;
    }
    @media (min-width: 1024px){
        div{
            width: 50%;
        }
    }
</style>