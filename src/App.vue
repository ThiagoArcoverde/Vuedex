<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokedex-logo.png">
      <hr>
      <input type="text" placeholder="Campo de busca por nome" v-model="busca" class="input is-rounded">
      <button class="button is-fullwidth is-success" id="busca-btn" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :dexNumber="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon.vue'
export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function () {
    // get pokeapi info
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151offset=0").then(response => {
      this.pokemons = response.data.results
      this.filteredPokemons = response.data.results
      console.log(this.pokemons)
    })
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons
      if(this.busca == '' | this.busca == ' '){
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.toLowerCase() == this.busca.toLowerCase())
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
#busca-btn{
  margin-top: 3%;
  margin-bottom: 3%;
  width: 33%;
  margin-left: auto;
  margin-right: auto;
}
</style>
