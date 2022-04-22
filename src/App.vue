<template>
  <div id="App">
    <div class="column is-half is-offset-one-quarter">
      <input type="text" class="input is-rounde" style="margin-bottom: 2%; " placeholder="Pesquisar" v-model="busca">
      <button class="button is-fullwidth is-success">Buscar</button>
      <div v-for="(poke, index) in resultadoBusca" :key="index">
        <PokeMon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PokeMon from "./components/PokeMon";


export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      busca: '',
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
      })
      .catch((e) => console.log(e));
  },
  components: {
    PokeMon,
  },
  computed:{
    resultadoBusca: function(){
      if(this.busca == ''|| this.busca == ` `){
        return this.pokemons;
      }else{
        console.log(this.busca)
       
        return this.pokemons.filter(p =>{p.name == this.busca})
      }
    }
  }
};
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
