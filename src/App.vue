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

    <button @click="AnimeRecommendations">Recomendaciones de Anime</button>
    <div v-if="animeRecommendations">
      <div v-for="recommendation in animeRecommendations" :key="recommendation.entry.mal_id">
        <h2>{{ recommendation.entry.title }}</h2>
        <a :href="recommendation.entry.url" target="_blank">Ver en MyAnimeList</a>
        <p>{{ recommendation.content }}</p>
      </div>
    </div>

    <button @click="CountryPopulation">Country Population</button>
    <div v-if="countryPopulation">
      <div v-for="country in countryPopulation" :key="country.country">
        <h2>{{ country.country }}</h2>
        <ul>
          <li v-for="population in country.populationCounts" :key="population.year">
            Year: {{ population.year }}, Population: {{ population.value }}
          </li>
        </ul>
      </div>
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
      animeRecommendations: [],
      countryPopulation: null,
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
    async AnimeRecommendations() {
      try {
        const response = await axios.get('https://api.jikan.moe/v4/recommendations/anime');
        this.animeRecommendations = response.data.data;
      } catch (error) {
        console.error("Error al obtener recomendaciones de anime:", error);
      }
    },
    async CountryPopulation() {
      try {
        const response = await axios.get('https://countriesnow.space/api/v0.1/countries/population');
        this.countryPopulation = response.data.data;
      } catch (error) {
        console.error("Error al obtener datos de población:", error);
      }
    },
  }
};
</script>

<style>

</style>