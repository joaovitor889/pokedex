<!-- eslint-disable vue/multi-word-component-names -->

<template>
  <div id="pokemon">

    <div id="borda" class="card ">
      <div class="card-image">
        <figure >
          <img :src="currentImg" alt="Placeholder image">
        </figure>
      </div>
      <div class="card-content has-background-danger">
        <div class="media">
          <div class="media-content ">
            <p class="title is-4 has-text-white">{{num}} - {{upper(name)}}</p>
            <p class="subtitle is-6 has-text-white">{{ pokemon.type }}</p>
            <button class="button is-medium is-fullwidth" @click="mudarSprite">{{ lado }}</button>
          </div>
        </div>
        <div class="content">
        </div>
      </div>
    </div>



  </div>
</template>

<script>
import axios from 'axios';


export default {
    created: function(){
      axios.get(this.url).then(res => {
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.currentImg = this.pokemon.front;

      })
    },
    data(){
      return{
        lado: 'De frente',
        isFront: true,
        currentImg: '',
        pokemon:{
          type: '',
          front: '',
          back: ''
        }
      }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    methods:{
      upper: function(value){
        var newName = value[0].toUpperCase() + value.slice(1);
        return newName
      },
      mudarSprite: function(){
        if(this.isFront){
          this.isFront = false;
          this.currentImg = this.pokemon.back;
          this.lado = "De costa";
        }else{
          this.isFront = true;
          this.currentImg = this.pokemon.front;
          this.lado = "De frente";
        }
      }
    } 
}
</script>

<style>
  #pokemon{
    margin-top: 2%;
  }
  #borda{
    border: solid #000 0.1rem;
    border-radius: 0.3rem;
  }
</style>