<template>
  <div id="app">    
    <div class="column is-half is-offset-one-quarter">
      <img class="pokedex" src="./assets/pokedex.png">
      <h1 class="is-size-3">Pokedex</h1>

      <div class="buscaPokemon">
        <input class="input is-success" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca">
      </div>

      <div v-for="(poke, index) in resultadoBusca" :key="poke.url">
        <pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
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
      busca: ''
    }
  },
  components: {
    Pokemon
  },
  computed: {
    resultadoBusca() {
      if(this.busca == '' || this.busca == ' ') {
        return this.pokemons
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  async created() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results
    })
  }
}
</script>

<style>
#app {
  font-family: Montserrat, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.pokedex {
  margin-top: 25px;
  width: 480px;
}

.is-size-3 {
  margin-top: -40px;
  
}
</style>
