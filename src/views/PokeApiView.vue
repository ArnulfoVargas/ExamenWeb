<script setup>
    import { watch, ref, onMounted } from "vue"
    import LoadingApi from "../components/PokeApi/LoadingApi.vue";
    import InputFieldsApi from "../components/PokeApi/InputFieldsApi.vue";
    import CartoonSubtitle from "../components/CartoonSubtitle.vue";
    import PokemonImage from "../components/PokeApi/PokemonImage.vue";
    import uniqid from "uniqid"

    const endpoint = 'https://pokeapi.co/api/v2/pokemon/';
    let current_data = ref(Math.floor(Math.random() * 1017 + 1).toString())

    const pokeapiData = ref({});
    const isLoading = ref(false);
    const error = ref(null);
    const images = ref({});
    const abilities = ref([])
    const types = ref([])

    const fetchData = async(data) => {
        isLoading.value = true;
        try{
            const response = await fetch(`${endpoint}${current_data.value}`)
            const data = await response.json();
            pokeapiData.value = {...data};
            images.value = {...data.sprites};
            abilities.value = [...data.abilities];
            types.value = [...data.types];
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

    const onNext = () => {
        const id = pokeapiData.value.id;

        if (id < 1017)
            current_data.value = id + 1;
    }

    const onPrev = () => {
        const id = pokeapiData.value.id;

        if (id > 0)
            current_data.value = id - 1;
    }
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

            <div class="data-container">
                <div>
                    <CartoonSubtitle>Abilities</CartoonSubtitle>
                    <p v-for="ability in abilities"
                        :key="uniqid()"
                    >
                        {{ ability.ability.name }}
                    </p>
                </div>

                <div>
                    <CartoonSubtitle>Types</CartoonSubtitle>
                    <p v-for="type in types"
                        :key="uniqid()"
                    >
                        {{ type.type.name }}
                    </p>
                </div>
            </div>

            <div class="buttons-holder">
                <button @click="onPrev" class="button">Prev</button>
                <button @click="onNext" class="button">Next</button>
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

    .data-container{
            width: 100%;
            display: grid;
            grid-template-rows: repeat(1, 1fr);
            justify-content: center;
            margin-top: 1rem;
        } 

    @media (min-width: 768px) {
        .data-container{
        grid-template-rows: auto;
        grid-template-columns: repeat(2, 350px);
    }
    }
    .data-container div{
        height: fit-content;
        display: flex;
        width: 100%;
        flex-direction: column;
        align-items: center;
        margin: 0;
        margin-bottom: .5rem;
    }

    .data-container div > p {
        text-transform: capitalize;
        margin: 0.1rem;
    }
    
    .button:hover{
        color: var(--color-white);
        background-color: var(--color-red);
        box-shadow: var(--box-shadow);
    }
</style>