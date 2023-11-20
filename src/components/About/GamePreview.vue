<script setup>
    import { ref, computed } from 'vue'
    import CartoonSubtitle from '../CartoonSubtitle.vue';
    import Slider from './Slider.vue';
    import CustomHR from '../CustomHR.vue';
    import CustomButton from './CustomButton.vue';
    
    const props = defineProps({
        data: {
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    })

    const reversed = computed(() => {
        return props.index % 2 == 1 ? 'reversed' : ''
    })

</script>

<template>
    <div class="body">
        <div class="container" :class="reversed">
            <div class="data-container">
                <CartoonSubtitle>{{ data.name }}</CartoonSubtitle>
                <p>{{ data.content }}</p>
                <CustomButton :url="data.url">Play</CustomButton>
            </div>

            <div class="image-container">
                <Slider :images="data.images"/>
            </div>

            
        </div>
        <CustomHR/>
    </div>
</template>

<style scoped>
    p{
        color: var(--color-gray);
        font-size: 1.25rem;
        line-height: 1.75rem;
        font-family: var(--main-font);
        text-align: center;
        margin-top: 1.25rem;
        margin-bottom: 1.25rem;
    }

    .body{
        width: 100%;
    }

    .container{
        width: 100%;
        height: fit-content;
        display: flex;
        padding: 0;
        margin: auto;
        justify-items: center;
        flex-direction: column;
        gap: 1.25rem;
    }

    .container.reversed{
        flex-direction: column;
    }

    .data-container{
        width: 90%;
        margin: auto;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .image-container{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 90%;
        margin: auto;
    }

    @media (min-width: 1024px){
        .container{
            width: 90%;
            padding: 2.5rem 0;
            gap: 0;
            flex-direction: row;
        }
        .container.reversed{
            flex-direction: row-reverse;
        }

        .data-container{
            width: 50%;
        }

        .image-container{
            width: 50%;
        }
    }
</style>