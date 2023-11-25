<script setup>
    import CartoonSubtitle from '../components/CartoonSubtitle.vue';
    import InputField from '../components/Contact/InputField.vue';

    import {reactive} from 'vue'

    const baseObjetct = {
        name: "",
        email: "",
        message:""
    }

    const userData = reactive({...baseObjetct})

    const onSubmit = (e) => {
        e.preventDefault();
        
        const data = {...userData};

        Object.assign(userData, baseObjetct);
    }
</script>

<template>
    <div>
        <CartoonSubtitle>Contact Me!</CartoonSubtitle>

        <div class="form-container">
            <InputField :label="'Name'" :placeholder="'Your name'" name="name" :inputType="'text'" v-model:data="userData.name"/>
            <InputField :label="'Email'" :placeholder="'Your email'" name="email" :inputType="'email'" v-model:data="userData.email"/>

            <textarea name="message" cols="30" rows="10" placeholder="Your message here" v-model="userData.message">

            </textarea>

            <button @click="onSubmit">Send!</button>
        </div>

        <p>{{ userData }}</p>
    </div>
</template>

<style scoped>
    
    .form-container{
        margin: auto;
        width: 90%;
        max-width: 500px;
    }

    textarea{
        margin-top: .5rem;
        margin-bottom: 1rem;
        width: calc(100% - 20px);
        resize: vertical;
        border: var(--thin-border);
        box-shadow: var(--box-shadow);
        color: var(--color-gray);
        font-family: var(--titles-font);
        font-size: 1.25rem;
        padding: 10px;
    }

    textarea:focus{
        outline: none;
    }

    textarea::placeholder{
        font-family: var(--titles-font);
        font-size: 1.25rem;
        margin: 0;
        color: rgba(57 52 52/ 0.5);
    }

    button{
        margin-left: 50%;
        transform: translateX(-50%);
        text-decoration: none;
        color: var(--color-red);
        background-color: var(--color-white);
        border: solid var(--color-red) .25rem;
        font-family: var(--main-font);
        font-weight: bold;
        font-size: 2rem;
        cursor: pointer;
        margin-bottom: 1rem;
        box-shadow: 0;

        transition-property: background-color, border, color, box-shadow;
        transition-duration: 125ms;
        transition-timing-function: linear;
    }

    button:hover{
        color: var(--color-white);
        background-color: var(--color-red);
        border: solid var(--color-red) .25rem;

        box-shadow: var(--box-shadow);
    }
</style>