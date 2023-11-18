<script setup>
  import uniqid from 'uniqid'

  import { GamesData, Pages } from "../data/data"
  import GamePreview from "../components/About/GamePreview.vue";
  import PagePreview from "../components/About/PagePreview.vue"
  import CatoonTitle from '../components/CatoonTitle.vue';
</script>

<template>
  <div class="body">
    <CatoonTitle>My Games</CatoonTitle>
    <div class="separator"></div>
    <GamePreview
      v-for="(data, index) in GamesData" :key="uniqid()"
      :data="data"
      :index="index"
    />

    <CatoonTitle>My Pages</CatoonTitle>

    <PagePreview 
      v-for="(data, index) in Pages" :key="uniqid()"
      :data="data"
      :index="index + GamesData.length "
    />
  </div>
</template>

<style>
  .separator{
    height: 10px;
    width: 100%;
  }

  @media (min-width: 1024px) {
    .separator{
      height: 0;
    }
  }
</style>