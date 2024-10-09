<template>
  <div>
    <h1>API Data Fetcher</h1>

    <button @click="RandomAnime">Anime Aleatorio</button>
    <p v-if="randomAnime">{{ randomAnime.title }}</p>
    <img v-if="randomAnime" :src="randomAnime.images.jpg.image_url" alt="Anime Image">
    <a v-if="randomAnime" :href="randomAnime.url" target="_blank">Ver en MyAnimeList</a>
    <p v-if="randomAnime">{{ randomAnime.synopsis }}</p>

    <button @click="RandomManga">Manga Aleatorio</button>
    <p v-if="randomManga">{{ randomManga.title }}</p>
    <img v-if="randomManga" :src="randomManga.images.jpg.image_url" alt="Manga Image">
    <a v-if="randomManga" :href="randomManga.url" target="_blank">Ver en MyAnimeList</a>
    <p v-if="randomManga">{{ randomManga.synopsis }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      randomAnime: null,
      randomManga: null,
      animeByCountryAndYear: null,
      mangaByCountryAndYear: null,
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
        this.randomManga = response.data.data;
      } catch (error) {
        console.error("Error al obtener manga aleatorio:", error);
      }
    },
  }
};
</script>

<style>

</style>