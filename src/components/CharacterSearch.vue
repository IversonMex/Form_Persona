<template>
  <div class="max-w-screen-xl mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Buscar personajes de Rick and Morty</h1>
    <form class="mb-4" @submit.prevent="searchCharacters">
      <input
        type="text"
        class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
        placeholder="Buscar personajes..."
        v-model="searchTerm"
      />
    </form>
    <ul>
      <li v-for="character in characters" :key="character.id" class="mb-4">
        <div class="flex items-center">
          <img :src="character.image" class="w-20 h-20 rounded-full mr-4" />
          <div>
            <h2 class="text-xl font-bold">{{ character.name }}</h2>
            <p class="text-gray-500">{{ character.species }} - {{ character.status }}</p>
            <button class="mt-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="showCharacterDetails(character)">Detalles</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
  <div class="fixed top-0 left-0 w-full h-full flex justify-center items-center bg-black bg-opacity-50" v-if="selectedCharacter">
      <div class="bg-white p-4 rounded-lg">
        <button class="absolute top-0 right-0 p-2" @click="hideCharacterDetails">
          <svg class="w-6 h-6 text-gray-500" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
            <path
              fill-rule="evenodd"
              d="M11.414 10l3.293-3.293a1 1 0 10-1.414-1.414L10 8.586 6.707 5.293a1 1 0 10-1.414 1.414L8.586 10l->">
            </path>
          </svg>
        </button>
      </div>
  </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        searchTerm: '',
        characters: [],
      };
    },
    methods: {
      async searchCharacters() {
        const response = await axios.get(
          `https://rickandmortyapi.com/api/character/?name=${this.searchTerm}`
        );
        this.characters = response.data.results;
      },
    },
  };
  </script>  