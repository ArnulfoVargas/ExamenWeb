<script setup>
    import { onMounted, ref } from 'vue';

    const props = defineProps({
        inputType: {
            type: String,
            required: true,
        },
        placeHolder: {
            type: String,
            required: true,
        },
        data: {
            type: Number || String,
            required: true,
        }
    })

    const emits = defineEmits(['update:data'])

    const input = ref(null);

    onMounted(() => {
        input.value.focus();
    })
    
    const search = () => {
        const result = input.value.value;
        if (props.inputType == 'text'){
            emits("update:data" ,result.toLowerCase())
        }
        else{
            emits('update:data', result)
        }
    }
</script>

<template>
    <div class="input-container">
        <input 
            ref="input" 
            :type="inputType" 
            :placeholder="placeHolder"
            >

        <button
            @click="search"
            >
            Search
        </button>
    </div>
</template>

<style scoped>
    .input-container{
        display: grid;
        grid-template-columns: 2fr 1fr;
        width: 83.33%;
        height: 3rem;
        box-shadow: var(--box-shadow);
        border: var(--thin-border);
    }

    input{
        width: 100%;
        border: solid 1px rgb(57, 52, 52);
        font-size: 1.5rem;
        line-height: 2rem;
        padding: 0 .5rem;
        font-family: var(--main-font);
    }

    input::placeholder{
        font-weight: bolder;
        color: rgba(57 52 52/ 0.5);
    }

    input:focus{
        outline: none;
    }

    button{
        background-color: var(--color-white);
        color: var(--color-red);
        border: none;
        font-family: var(--main-font);
        border: solid 1px rgb(57, 52, 52);
        font-weight: bold;
        cursor: pointer;
        border-radius: 0;
        font-size: 1.25rem;
        
        transition-property: background-color, color;
        transition-duration: 125ms;
        transition-timing-function: linear;
    }

    button:hover{
        color: var(--color-white);
        background-color: var(--color-red);
    }

    @media (min-width: 768px) {
        .input-container{
            padding: 0;
            width: 24rem;
        }
    }
</style>