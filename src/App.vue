<template>
  
  <div id="app">
    <Navbar/>
    <div class="column is-half is-offset-one-quarter">
      <input type="text" name="" id="" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-rounded ">
      <button class="button is-fullwidth is-dark is-outlined" id="buscaBtn" @click="buscar">Pesquisar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
      </div>
    </div>

   

  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from "./components/Pokemon.vue";
import Navbar from './components/Navbar.vue';
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista de pokemons");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components:{
    Pokemon,
    Navbar
  },
  methods:{
    buscar: function(){
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }

  },
  computed:{
    // resultadoBusca: function(){
    //   if(this.busca == ''|| this.busca==' '){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
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
}
#buscaBtn{
  margin-top: 2%;
}
</style>
