<template>
  <div id="app">
    <div v-for="(poke,index) in pokemon" :key="index">
      <pokemons :numero="(index+1)" :name="poke.name" :url="poke.url"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import pokemons from './components/pokemons';
export default {
  name: 'App',
  components: {
    pokemons
  },
  data(){
    return{
      pokemon:[]
    }
  },
  created: function(){
    axios.get(' https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res=>{
      console.log("Pegou a lista de pokemons")
      this.pokemon=res.data.results
    })
  },
}
</script>

<style>
  #app{
    text-align: center;
  }
</style>
