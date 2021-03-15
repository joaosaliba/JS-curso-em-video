<template>
  <div id="pokemon">
    <h1> </h1>
    <img src="poekmon.front" alt="">


    <div class="card" >
  <div class="card-image">
    <figure >
      <img :src="currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      
      </div>
      <div class="media-content">
        <p class="title is-4">{{ num }} - {{ name | upper }}</p>
        <p class="subtitle is-6">{{pokemon.type}}</p>
      </div>
    </div>

    <div class="content">
        <button class="button is-medium is-fullwidth" @click="mudarSprit" >Mudar Sprit</button>
    </div>

  </div>
</div>
  
</template>

<script>
import axios from "axios";

export default {
  created: function(){
      const vm = this;
      axios.get(vm.url)
      .then(function(response){
          vm.pokemon.type= response.data.types[0].type.name;
          vm.pokemon.front = response.data.sprites.front_default;
          vm.pokemon.back = response.data.sprites.back_default;
          vm.currentImg=vm.pokemon.front;
          console.log(vm.pokemon)

      })
  },

    data(){
        return{
            isFront:true,
            currentImg:'',
            pokemon:{
                type:'',
                front:'',
                back:'',

            },
        }
    },

  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: function (value) {
      const newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods:{
      mudarSprit: function(){
          const vm= this;
          if(vm.isFront){
              vm.isFront =false;
              vm.currentImg= vm.pokemon.back
          }else{
              vm.isFront=true;
              vm.currentImg= vm.pokemon.front
          }
      }
  }
};
</script>

<style>
#pokemon{
    margin-top: 2%;
}
/* .card{
    width:50%
} */
</style>