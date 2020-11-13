<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/breno.png" alt="">
      <h1 class="is-size-6">POKEDEX</h1>
      <input type="text" v-model="search" class="input is-rounded"
      placeholder="search a pokemon by the name">
      <br>
      <br>
      <button class="button is-fullwidth is-success">Search</button>
      <br>
      <div v-for="(pokemon, index) in searchPokemons" :key="pokemon.name">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      search: ''
    }
  },
  created: async function() {
    const pokemons = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
    this.pokemons = pokemons.data.results
  },
  components: {
    Pokemon
  },
  computed: {
    searchPokemons: function() {
      if(!this.search.trim()) {
        return this.pokemons
      } else {
        const regex = new RegExp(this.search)
        return this.pokemons.filter(pokemon => pokemon.name.match(regex))
      }
    }
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
