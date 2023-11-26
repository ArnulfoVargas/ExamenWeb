<script setup>
    import { supabase } from '../lib/supabaseClient';
    import { reactive, ref, onMounted } from 'vue'

    import CartoonSubtitle from '../components/CartoonSubtitle.vue';
    import ErrorMessage from '../components/Contact/ErrorMessage.vue';
    import InputField from '../components/Contact/InputField.vue';
    import DataSendedMessage from '../components/Contact/DataSendedMessage.vue';

    const baseObjetct = {
        name: "",
        email: "",
        message:""
    }

    const nameErr = ref("");
    let nameTimeout;
    const emailErr = ref("");
    let emailTimeout;
    const sendErr = ref("");
    let sendErrTimeout;

    const emailSend = ref(false);
    let emailSendTimeout;

    const userData = reactive({...baseObjetct})

    onMounted(()=>{
        emailjs.init('ovbHGIs4yA_pFc8Bz');
    })

    const validateName = (formData) =>{
        if (formData.name === ""){
            nameErr.value = "Empty Name not Valid"
            if (nameTimeout){
                clearTimeout(nameTimeout)
            }

            nameTimeout = setTimeout(() => {
                nameErr.value = ""
            }, 2000)

            return false
        }

        return true;
    }

    const validateEmail = (formData) => {
        if (formData.email === "" ){
            emailErr.value = "Empty Email not valid"
        }
        else{
            let regex = /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/;
            if (!regex.test(formData.email)){
                emailErr.value = "Type a valid Email"
            }
        }
        
        if(emailErr.value != ""){
            if (emailTimeout){
                clearTimeout(emailTimeout)
            }

            emailTimeout = setTimeout(() => {
                emailErr.value = ""
            }, 2000)

            return false
        }
        
        return true;
    }

    const onEmailSend = () => {
        emailSend.value = true;
        
        if (emailSendTimeout){
                clearTimeout(emailSendTimeout)
            }

            emailSendTimeout = setTimeout(() => {
                emailSend.value = false;
            }, 2000)
    }

    const handleError = () => {
        sendErr.value = "err";
        
        if (sendErrTimeout){
                clearTimeout(sendErrTimeout)
            }

            sendErrTimeout = setTimeout(() => {
                sendErr.value = "";
            }, 2000)
    }

    const onSubmit = async() => {
        let canSend = true;

        const formData = {...userData};
        formData.name = formData.name.trim();
        formData.email = formData.email.trim();
        formData.message = formData.message.trim();

        canSend = validateName(formData);
        canSend = validateEmail(formData);

        if (!canSend) return
        
        const { data, error } = await supabase
            .from('users')
            .insert([
                    { name: `${formData.name}`, email:`${formData.email}`, message: `${formData.message}` },
                ])
            .select()

        if (error) {
            handleError()
            return
        }

        const service_id = "service_w0pzwiu"
        const template_id = "template_tyx1pvq"
        await emailjs.send(service_id, template_id, {to: formData.email});

        Object.assign(userData, baseObjetct);
        onEmailSend();
    }
</script>

<template>
    <div>
        <CartoonSubtitle>Contact Me!</CartoonSubtitle>

        <div class="form-container">
            <InputField 
                :label="'Name'" 
                :placeholder="'Your name'" 
                :inputType="'text'" 
                name="name" 
                v-model:data="userData.name"
                />
            
            <ErrorMessage :error="nameErr != ''">{{ nameErr }}</ErrorMessage>

            <InputField 
                :label="'Email'" 
                :placeholder="'Your email'" 
                :inputType="'email'" 
                name="email" 
                v-model:data="userData.email"
                />

            <ErrorMessage :error="emailErr != ''">{{ emailErr }}</ErrorMessage>

            <textarea 
                name="message" 
                cols="30" rows="10" 
                placeholder="Your message here" 
                v-model="userData.message"
                maxlength="255"
                >

            </textarea>

            <DataSendedMessage :sended="emailSend"/>

            <button @click="onSubmit">Send!</button>
        </div>
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