<template>
  <div class="card">
    <div class="card-image">
      <figure>
        <img :src="pokemon.front" alt="Placeholder image">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ index }}. {{ name | upperCase }}</p>
          <p class="subtitle is-6">{{ pokemon.type }}</p>
        </div>
      </div>
      <div class="content"></div>
    </div>
  </div>
</template>

<script>
import api from '../services/api';

export default {
  name: 'Pokemon',
  props: {
    index: Number,
    name: String
  },
  created: function() {
    api.get(`pokemon/${this.index}`).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
    });
  },
  data() {
    return {
      pokemon: {
        type: '',
        front: '',
        back: '',
      }
    }
  },
  filters: {
    upperCase: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}
</script>

<style>
  .card {
    margin-top: 1vh;
  }
</style>

