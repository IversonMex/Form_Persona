<script>
import CharacterSearch from './CharacterSearch.vue';
import axios from 'axios'

let API_URL = 'https://rickandmortyapi.com/api/character'

export default {
  name: 'App',
  components: {
    CharacterSearch,
  },
  data() {
    return {
      info: [],
      personajes: [],
      cont:2
    }
  },

  mounted() {
    axios.get(API_URL)
      .then((response) => {
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
  },

  methods: {
    pag(num) {
      API_URL='https://rickandmortyapi.com/api/character/?page='+num
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
      this.cont++
    }
  },

}

</script>

<template>
  <CharacterSearch />
  <h2>Hay {{ info.count }} personajes en el programa de Rick & Morty</h2>
  <button @click="pag(cont)">página {{ cont }}</button>
  <ul>
    <li v-for="p in personajes">
      <a >{{ p.name }} id:{{ p.id }}</a> 
    </li>
  </ul>
</template>