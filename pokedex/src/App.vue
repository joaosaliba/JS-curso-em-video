<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <input type="text" placeholder="Busque o Pokemin Pelo nome" class="input is-rounded"  v-model="busca">
      <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar" >Buscar</button>
    <div v-for="(pokemon,index) in filteredPokemons" :key="pokemon.url">
      <Pokemon :name="pokemon.name" :num="index+1" :url="pokemon.url" />
    </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios';

import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data(){
    return{
      pokemons:[],
      filteredPokemons:[],
      busca:'',
    }
  },

  created: function(){
    const vm =this;
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
    .then(function(response){
      vm.pokemons = response.data.results; 
      vm.filteredPokemons = response.data.results;
      console.log("Get works"); 
    })
  },
  components:{
    Pokemon,
    
  },
  methods:{
    buscar:function(){
      const vm = this;
      vm.filteredPokemons=vm.pokemons;

       if(vm.busca =='' || vm.busca== ' '){ 
         vm.filteredPokemons =vm.pokemons;
        }else{
        vm.filteredPokemons= vm.pokemons.filter(pokemon=> pokemon.name ==vm.busca);
        }

    }
  }
  // computed:{
  //   resutladoBusca: function(){
  //      const vm = this;
  //      if(vm.busca =='' || vm.busca== ' '){
  //        return vm.pokemons
  //      }else{
  //        return vm.pokemons.filter(pokemon=> pokemon.name ==vm.busca)
  //      }
  //   }
  // }
  
}
</script>

<style>
#buscaBtn{
  margin-top: 2%;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /* background: #2c3e50; */
  margin-top: 60px;
}
</style>
