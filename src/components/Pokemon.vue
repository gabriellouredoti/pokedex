<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" alt="Placeholder image">
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{num}} {{name}}</p>
            <p class="subtitle is-6">{{pokem.type}}</p>
          </div>
        </div>
        <div class="content">
          <button class="button is-medium is-fullwidth" @click="trocarImagem">Mudar sprite</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">

import axios from 'axios';

export default{
  created: function(){
    axios.get(this.url).then(res => {
      this.pokem.type = res.data.types[0].type.name;
      this.pokem.front = res.data.sprites.front_default;
      this.pokem.back = res.data.sprites.back_default;
      this.currentImg = this.pokem.front;
      
    
    })
  },
  data(){
    return{
      isFront: true,
      currentImg: '',
      pokem: {

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
  methods: {
    trocarImagem: function(){
      if(this.isFront == true){
        this.isFront = false;
        this.currentImg = this.pokem.back;
      }else{
        this.isFront = true;
        this.currentImg = this.pokem.front;
      }
    }
  }
  
}
</script>

<style>
  #pokemon{
    margin-top: 3%;

  }
</style>