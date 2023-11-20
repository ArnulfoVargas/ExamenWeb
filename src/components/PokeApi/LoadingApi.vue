<script setup>
    import CatoonTitle from '../CatoonTitle.vue';
    import {ref, onUnmounted, onMounted} from 'vue';

    let interval = null;
    const baseText = "Loading";
    let current_index = 0;
    const loadingText = ref(baseText);

    onMounted(()=>{
        interval = setInterval(() => {
            current_index++;
            current_index %= 4;

            if(current_index == 0){
                loadingText.value = baseText;
                return;
            } 
            
            let str = "";
            for (let i = 0; i < current_index; i++){
                str += '.'
            }

            loadingText.value = baseText + str;

        }, 250)
    })

    onUnmounted(() => {
        if (interval != null){
            clearInterval(interval);
        }
    })
</script>
    
<template>
    <div class="container">
        <CatoonTitle>{{ loadingText }}</CatoonTitle>
    </div>
</template>

<style scoped>
    .container{
        height: calc(100dvh - 5rem);
        width: fit-content;
        margin: auto;
        display: flex;
        align-items: center;
    }
</style>