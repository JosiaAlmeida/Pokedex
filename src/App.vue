<template>
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter">
      <input type="text" placeholder="Pesquisa" v-model="busca" class="input is-rounded">
      <button class="button is-medium is-dark" id="btn" @click="buscar">Buscar</button>
      <div v-for="(poke,index) in filterbuscar" :key="poke.url">
        <pokemons :numero="(index+1)" :name="poke.name" :url="poke.url"/>
      </div>
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
      pokemon:[],
      filterbuscar:[],
      busca: ''
    }
  },
  created: function(){
    axios.get(' https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res=>{
      console.log("Pegou a lista de pokemons")
      this.pokemon=res.data.results
      this.filterbuscar=res.data.results
    })
  },
  methods:{
     buscar: function(){
       this.filterbuscar=this.pokemon
      if(this.busca==''|| this.busca==' '){
        this.filterbuscar= this.pokemon;
      }
      else{
         this.filterbuscar= this.pokemon.filter(pokemons=> pokemons.name==this.busca)
      }
    }
  },
  computed:{
    busc: function(){
      if(this.busca==''|| this.busca==' '){
        return this.pokemon;
      }
      else{
         //return this.pokemon.filter(pokemons => pokemons.name.match(this.busca))
        return this.pokemon.filter(pokemons=> pokemons.name==this.busca)
      }
    }
  }
}
</script>

<style>
  #app{
    text-align: center;
  }
  #btn{
    margin: 1%;
    padding: 1%;
  }
</style>
