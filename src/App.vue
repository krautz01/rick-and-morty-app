<template>
  <div id="app">
    <Filters @applyFilters="applyFilters" />
    <div class="characters">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character"
      />
    </div>
    <Pagination
      :currentPage="currentPage"
      :totalPages="totalPages"
      @pageChange="fetchCharacters"
    />
  </div>
</template>

<script>
import axios from "axios";
import CharacterCard from "./components/CharacterCard.vue";
import Pagination from "./components/Pagination.vue";
import Filters from "./components/Filters.vue";

export default {
  components: {
    CharacterCard,
    Pagination,
    Filters,
  },
  data() {
    return {
      characters: [],
      currentPage: 1,
      totalPages: 1,
      filters: {
        name: "",
        status: "",
      },
    };
  },
  methods: {
    async fetchCharacters(page = 1) {
      const { name, status } = this.filters;
      const response = await axios.get(
        "https://rickandmortyapi.com/api/character",
        {
          params: {
            page,
            name,
            status,
          },
        }
      );
      this.characters = response.data.results;
      this.currentPage = page;
      this.totalPages = response.data.info.pages;
    },
    applyFilters(filters) {
      this.filters = filters;
      this.fetchCharacters(1);
    },
  },
  created() {
    this.fetchCharacters();
  },
};
</script>

<!-- <template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> -->
