<script setup>
    import CartoonSubtitle from '../components/CartoonSubtitle.vue';
    import InputField from '../components/Contact/InputField.vue';

</script>

<template>
    <div>
        <CartoonSubtitle>Contact Me!</CartoonSubtitle>

        <div class="form-container">
            <InputField :label="'Name'" :placeholder="'Your name'" name="name"/>
            <InputField :label="'Email'" :placeholder="'Your email'" name="email"/>

            <textarea name="message" cols="30" rows="10" placeholder="Your message here" value="">

            </textarea>

            <button>Send!</button>
        </div>
    </div>
</template>

<style scoped>
    .form-container{
        margin: auto;
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
</style>