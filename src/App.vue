<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div :key="index" v-for="(pokemon, index) in pokemons">
        <Pokemon :index="index + 1" :name="pokemon.name" />
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
      pokemons: []
    }
  },
  // Função é executada quando a página é criada
  created: function() {
    api.get('pokemon?limit=151&offset=0').then((response) => { 
      this.pokemons = response.data.results;
    });
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
</style>
