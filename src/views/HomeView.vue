<script setup>
  import uniqid from 'uniqid'

  import CatoonTitle from '../components/CatoonTitle.vue';
  import CartoonSubtitle from '../components/CartoonSubtitle.vue';
  import HalfScreenBody from '../components/HalfScreenBody.vue';
  import TechCard from '../components/TechCard.vue';
  import CustomHR from '../components/CustomHR.vue';

  import { Languages, Tecnologies} from "../data/data"
</script>

<template>
  <div class="body">
    <CatoonTitle>Who am I?</CatoonTitle>
    
    <HalfScreenBody>
      Hello, my name is Arnulfo, I am a 19 year old young man who is currently studying Interactive Software and Video Game Development
      at the Amerike Institute. Despite my young age, I have been programming and developing software for about 3 years, which has led me 
      to experience and know a lot of technologies.
    </HalfScreenBody>

    <CartoonSubtitle>Languages</CartoonSubtitle>

    <HalfScreenBody>
      Next I will show the programming languages that I know ordered from the most used to the less used.
    </HalfScreenBody>

    <div class="container">
      <TechCard
        v-for="(lang) in Languages" :key="uniqid()" 
        :tech="lang.image"
        :docs="lang.docs"
        >{{ lang.name }}</TechCard>
    </div>
    
    <CustomHR/>

    <CartoonSubtitle>Technologies</CartoonSubtitle>

    <HalfScreenBody>
      Below I will show the technologies that I have used throughout my career.
    </HalfScreenBody>

    <div class="container">
      <TechCard
        v-for="(tech) in Tecnologies" :key="uniqid()" 
        :tech="tech.image"
        >{{ tech.name }}</TechCard>
    </div>

    <CustomHR/>

  </div>
</template>

<style scoped>
  .container{
    width: 75%;
    display: flex;
    gap: 2.5rem;
    flex-wrap: wrap;
    flex-direction: row;
    justify-content: center;
    margin: auto;
  }
</style>
