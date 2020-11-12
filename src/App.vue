<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.svg">
      <input class="input is-rounded" type="text" placeholder="Buscar pokémon" v-model="busca">
      <button class="button is-medium is-fullwidth is-rounded is-link" id="buscaBtn" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name | upper" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>

import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      busca: '',
      filteredPokemons: []
    }
  },

  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?offset=0&limit=151').
    then(res => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
        
      }
    )
  },

  components: {
    Pokemon
  },

  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
        
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemons => pokemons.name.toUpperCase() == this.busca.toUpperCase())
        
      }
    }
  },
  filters: {
    upper: function(value){

      var newname = value[0].toUpperCase() + value.slice(1);
      return newname;
    }
  },
  computed: {
    // results: function(){
    //   if(this.busca == '' || this.busca == ' '){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name.toUpperCase() == this.busca.toUpperCase());
    //   }
    // }


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

#buscaBtn{
  margin-top: 2%;
}

</style>
