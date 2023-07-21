<template>
  
  <div id="app">
    <Navbar/>
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, index) in pokemons" :key="index">
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
      pokemons: []
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista de pokemons");
      this.pokemons = res.data.results;
    })
  },
  components:{
    Pokemon,
    Navbar
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
</style>
