<script setup>
    import {defineProps, ref, computed} from 'vue'

    const props = defineProps({
        images: {
            type: Array,
            required: true
        }
    })

    let currentIndex = ref(0);
    let touchStartX = 0
    let touchEndX = 0

    const onNext = () => {
        currentIndex.value++;
        currentIndex.value %= props.images.length - 1;
    }

    const onPrev = () => {
        currentIndex.value--;
        if(currentIndex.value < 0)
            currentIndex.value = props.images.length - 1
    }

    const currentImage = computed(() => {
        return props.images[currentIndex.value]
    })

    const touchStart = (event) => {
        touchStartX = event.changedTouches[0].screenX
    }

    const touchEnd = (event) => {
        touchEndX = event.changedTouches[0].screenX

        const diference = Math.abs(touchStartX - touchEndX)

        if(diference < 40) return

        if (touchEndX < touchStartX) onPrev()
        if (touchEndX > touchStartX) onNext()
    }
</script>

<template>
    <div class="slider-container">
        <div class="slider" @touchstart="touchStart" @touchend="touchEnd">
            <div class="prev" @click="onPrev">&#10092;</div>
            <div class="next" @click="onNext">&#10093;</div>

            <div class="image-container">
                <img :src="currentImage" alt="screen-shot">
            </div>
        </div>
    </div>
</template>

<style scoped>
    .slider-container{
        width: 100%;
    }

    .slider{
        position: relative;
        height: fit-content;
    }

    .prev, .next{
        position: absolute;
        top: 50%;
        transform: translate(-50%);
        font-size: 1.875rem;
        color: var(--color-white);
        z-index: 1;
        cursor: pointer;
    }

    .prev{
        left: 2rem;
    }

    .next {
        right: 2rem;
    }

    .image-container{
        height: fit-content;
        width: 100%;
    }

    img{
        width: 100%;
        -webkit-user-drag: none;
    }

    @media (min-width: 1024px) {
        .slider-container{
            width: 75%;
        }
    }
</style>