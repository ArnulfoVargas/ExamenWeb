<script setup>
  import CatoonTitle from '../components/CatoonTitle.vue';
  import CartoonSubtitle from '../components/CartoonSubtitle.vue';
  import HalfScreenBody from '../components/HalfScreenBody.vue';
  import TechCard from '../components/TechCard.vue';
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
        :tech="'/Languages/js.png'" 
        >Java Script</TechCard>
      <TechCard 
        :tech="'/Tech/flutter.png'"
        >Flutter</TechCard>
    </div>
  </div>
</template>

<style scoped>
  .body{
    margin: auto;
    padding: 1.25rem 0;
  }

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
