<template>
  <div>
    <h1>API Data Fetcher</h1>

    <button @click="RandomAnime">Anime Aleatorio</button>
    <p v-if="randomAnime">{{ randomAnime.title }}</p>
    <img v-if="randomAnime" :src="randomAnime.image_url" alt="Anime Image">
    <a v-if="randomAnime" :href="randomAnime.url" target="_blank">Ver en MyAnimeList</a>
    <p v-if="randomAnime">{{ randomAnime.synopsis }}</p>

    <div v-if="animeByCountryAndYear">
      <p>{{ animeByCountryAndYear.title }}</p>
      <img :src="animeByCountryAndYear.image_url" alt="Anime Image">
      <a :href="animeByCountryAndYear.url" target="_blank">Ver en MyAnimeList</a>
      <p>{{ animeByCountryAndYear.synopsis }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      randomAnime: null,
      randomManga: null,
    };
  },
  methods: {
    async RandomAnime() {
      try {
        const response = await axios.get('https://api.jikan.moe/v4/random/anime');
        this.randomAnime = response.data.data;
      } catch (error) {
        console.error("Error al obtener anime aleatorio:", error);
      }
    },
    async RandomManga() {
      try {
        const response = await axios.get('https://api.jikan.moe/v4/random/manga');
        this.randomManga = JSON.stringify(response.data.data);
      } catch (error) {
        console.error("Error al obtener manga aleatorio:", error);
      }
    },
  }
};
</script>

<style>
</style>