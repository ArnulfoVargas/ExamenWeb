<script setup>
    import { watch, ref, onMounted } from "vue"
    import LoadingApi from "../components/PokeApi/LoadingApi.vue";
    import InputFieldsApi from "../components/PokeApi/InputFieldsApi.vue";
    import CartoonSubtitle from "../components/CartoonSubtitle.vue";
    import PokemonImage from "../components/PokeApi/PokemonImage.vue";

    const endpoint = 'https://pokeapi.co/api/v2/pokemon/';
    let current_data = ref(Math.floor(Math.random() * 1017 + 1).toString())

    let pokeapiData = ref({});
    let isLoading = ref(false);
    let error = ref(null);
    let images = ref({})

    const fetchData = async(data) => {
        isLoading.value = true;
        try{
            const response = await fetch(`${endpoint}${current_data.value}`)
            const data = await response.json();
            pokeapiData.value = {...data};
            images.value = {...data.sprites};
        }catch (err){
            error.value = err;
        }finally{
            isLoading.value = false;
        }
    }

    onMounted(async() => {
        await fetchData(current_data.value)
    })

    watch(current_data, async () => {
        await fetchData(current_data.value)
    })
</script>

<template>
    <div>
        <LoadingApi 
            v-if="isLoading"
            />
        <div v-else>
            <div class="inputs-container">
                <InputFieldsApi 
                    :input-type="'text'" 
                    :place-holder="pokeapiData.name"
                    v-model:data="current_data"
                    />

                <InputFieldsApi 
                    :input-type="'number'" 
                    :place-holder="pokeapiData.id"
                    v-model:data="current_data"
                    />
            </div>

            <CartoonSubtitle>{{ `${pokeapiData.name}`.toUpperCase() }}</CartoonSubtitle>
            <p>ID: {{ pokeapiData.id }}</p>

            <PokemonImage 
                :shiny-image="images.front_shiny"
                :normal-image="images.front_default"
                />

            <div class="buttons-holder">
                <button class="button">Prev</button>
                <button class="button">Next</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .inputs-container{
        margin: auto;
        gap: 1.5rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-top: 1.25rem;
        margin-bottom: 1.25rem;
    }

    @media (min-width: 768px) {
        .inputs-container{
            display: flex;
            flex-direction: row;
            width: 75%;
        }
    }

    p{
        color: var(--color-gray);
        text-align: center;
        font-size: 1.25rem;
        line-height: 1.75rem;
    }

    .buttons-holder{
        margin: 20px auto;
        width: calc(100% - 3.75rem);
        display: flex;
        justify-content: center;
        gap: 1.25rem;
        padding: 0 1.25rem;
    }

    @media (min-width: 768px) {
        .buttons-holder{
            margin: 20px auto;
            width: 60%;
            max-width: 1000px;
        }
    }

    .button{
        background-color: var(--color-white);
        color: var(--color-red);
        border: none;
        font-family: var(--main-font);
        border: solid 2px var(--color-red);
        font-weight: bold;
        cursor: pointer;
        border-radius: 0;
        font-size: 1.5rem;
        line-height: 2rem;
        box-shadow: none;

        width: 83.33%;
        height: 3rem;
        
        transition-property: background-color, color, box-shadow;
        transition-duration: 125ms;
        transition-timing-function: linear;
    }

    .button:hover{
        color: var(--color-white);
        background-color: var(--color-red);
        box-shadow: var(--box-shadow);
    }
</style>