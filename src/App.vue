<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png" alt="Pokemon Logo" width="30%">
      <input type="text" name="" id="" placeholder="Buscar Pokemon" class="input is-rounded" v-model="search">
      <button id="searchBtn" class="button is-fullwidth is-success is-rounded" @click="searchPokemons">Buscar</button>
    </div>
    <div>
      <div id="pokemon-list">
        <div :key="pokemon.url" v-for="(pokemon, index) in filteredPokemons">
          <Pokemon :index="index + 1" :name="pokemon.name" :url="pokemon.url" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import api from './services/api';
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  components: {
    Pokemon
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      search: ''
    }
  },
  // Função é executada quando a página é criada
  created: function() {
    api.get('pokemon?limit=151&offset=0').then((response) => { 
      this.pokemons = response.data.results;
      this.filteredPokemons = response.data.results;
    });
  },
  methods: {
    searchPokemons: function() {
      this.filteredPokemons = this.pokemons;
      if(this.search == '' || this.search == ' ') {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter((pokemon) => pokemon.name == this.search);
      }
    }
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

#searchBtn {
  margin-top: 1vh;
}

#pokemon-list {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
