<script setup>
    import { RouterView } from 'vue-router'

    defineProps({
        to: {
            type:String,
            required: true,
        }
    })

    defineEmits(["on-hide"])
</script>

<template>
    <RouterLink :to="to">
        <div 
            class="route"
            @click="$emit('on-hide')"
            >
            <p><slot></slot></p>
        </div>
    </RouterLink>
</template>

<style scoped>
    .route{
        height: 5rem;
        width: 100%;
        display: flex;
        justify-content: left;
        align-items: center;
        padding: 0 2.5rem;
        color: var(--color-white);
    }

    @media (min-width: 768px) {
        .route{
            justify-content: center;
            height: 100%;
            padding: 0;
            width: 8rem;
        }

        .route p{
            font-size: 1.125rem;
            line-height: 1.75rem;
        }
    }

    @media (min-width: 1024px) {
        .route p{
            font-size: 1.5rem;
            line-height: 2rem;
        }
    }

    .route:hover{
        background-color: #9f0c0c;
    }

    .route p{
        font-size: 1.5rem;
        color: var(--color-white);
        font-family: var(--titles-font);
        font-weight: bold;
    }
</style>