<template>
  <div>
    <h1>API</h1>

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

    <div v-if="animeByCountryAndYear">
      <p>{{ animeByCountryAndYear.title }}</p>
      <img :src="animeByCountryAndYear.images.jpg.image_url" alt="Anime Image">
      <a :href="animeByCountryAndYear.url" target="_blank">Ver en MyAnimeList</a>
      <p>{{ animeByCountryAndYear.synopsis }}</p>
    </div>

    <div v-if="mangaByCountryAndYear">
      <p>{{ mangaByCountryAndYear.title }}</p>
      <img :src="mangaByCountryAndYear.images.jpg.image_url" alt="Manga Image">
      <a :href="mangaByCountryAndYear.url" target="_blank">Ver en MyAnimeList</a>
      <p>{{ mangaByCountryAndYear.synopsis }}</p>
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
    async fetchAnimeByCountryAndYear(country, year) {
      try {
        const response = await axios.get(`https://api.jikan.moe/v4/anime?country=${country}&year=${year}`);
        this.animeByCountryAndYear = response.data.data[0];
      } catch (error) {
        console.error("Error al obtener anime por país y año:", error);
      }
    },
    async fetchMangaByCountryAndYear(country, year) {
      try {
        const response = await axios.get(`https://api.jikan.moe/v4/manga?country=${country}&year=${year}`);
        this.mangaByCountryAndYear = response.data.data[0];
      } catch (error) {
        console.error("Error al obtener manga por país y año:", error);
      }
    }
  }
};
</script>

<style>

</style>