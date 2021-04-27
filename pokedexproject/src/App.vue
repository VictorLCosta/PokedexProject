<template>
  <div id="app">
    <input type="text" placeholder="" v-model="query" class="input is-rounded">
    <button class="button is-primary is-fullwidth"></button>
    <div v-for="(poke, index) in queryResult" :key="index" >
      <div class="column is-two-fifths"><Poke :name="poke.name" :url="poke.url" :num="index+1" /></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Poke from './components/Poke'
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      query: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=100&offset=200').then(res => {
      this.pokemons = res.data.results;
    })
  },
  components: {
    Poke
  },
  computed: {
    queryResult: function(){
      if(this.query == '' || this.query == ' '){
        return this.pokemons;
      }
      else{
        return this.pokemons.filter(pokemon => pokemon.name == this.query)
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
</style>
