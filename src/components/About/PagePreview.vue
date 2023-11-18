<script setup>
    import { computed, ref, onMounted } from 'vue'
    import CartoonSubtitle from '../CartoonSubtitle.vue';
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

    let frame = ref(null);

    onMounted(() => {
        frame.value.focus()
        frame.value.muted=true;
    })


</script>

<template>
    <div class="body">
        <div class="container" :class="reversed">
            <div class="data-container">
                <CartoonSubtitle>{{ data.name }}</CartoonSubtitle>
                <p>{{ data.content }}</p>
                <CustomButton :url="data.url">Visit</CustomButton>
            </div>

            <div class="page-container">
                <iframe ref="frame" :src="data.url"></iframe>
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

    .page-container{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 90%;
        margin: auto;
        aspect-ratio: 16 / 9;
    }

    .page-container iframe{
        width: 80%;
        height: 80%;
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

        .page-container{
            width: 50%;
        }
    }
</style>