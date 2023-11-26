<script setup>
    defineProps({
        label: String,
        placeholder: String,
        inputType:String,
        data:String,
        pattern: String,
    })

    const emits = defineEmits(["update:data"])
</script>

<template>
    <div class="container">
        <div>
            <p>{{ label }}</p>
        </div>

        <input 
            :type="inputType" 
            :placeholder="placeholder" 
            :value="data" 
            @input="$emit('update:data', $event.target.value)"
            maxlength="50"
            required
            >
    </div>
</template>

<style scoped>
    .container{
        display: grid;
        height: 3rem;
        grid-template-columns: 1fr 2fr;
        border: var(--thin-border);
        margin-top: .5rem;
        box-shadow: var(--box-shadow);
    }

    .container > div{
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: var(--color-red);
    }
    
    input{
        border-radius: 0;
        border: none;
        border-left: var(--thin-border);
        color: var(--color-gray);
        font-family: var(--titles-font);
        font-size: 1.5rem;
        margin: 0;
        padding-left: 10px;
    }

    input:focus{
        outline: none;
    }

    input::placeholder{
        font-family: var(--titles-font);
        font-size: 1.5rem;
        margin: 0;
        color: rgba(57 52 52/ 0.5);
    }

    .top-none{
        border-top: none;
    }

    p{
        color: var(--color-white);
        font-family: var(--main-font);
        font-size: 1.5rem;
        margin: 0;
        font-weight: bold;
    }
</style>