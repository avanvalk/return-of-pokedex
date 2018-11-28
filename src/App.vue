
<template>
  <div id="app">
    <Header 
      v-bind:sort="sort" 
      v-bind:filter="filter" 
      />

    <Pokemons v-bind:pokemons="sorted"/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import pokemonApi from '../pokemonApi';
import Pokemons from './components/Pokemons.vue';


export default {

  data() {
    return {
      pokemons: pokemonApi.getPokemon(),
      filter: {
        name:"",
        type_1: "",
        attack: "",
        defense: ""
      },
      sort: {
        field: 'name',
        direction: 1
      }
    };
  },
  components: {
    Header,
    Pokemons
  },
  computed: {
    filtered() {
      return this.pokemons.filter(pokemon => {
        const hasName = !this.filter.name || pokemon.pokemon >= this.filter.name;
        const hasType = !this.filter.type_1 || pokemon.type_1 === this.filter.type_1;
        const hasAttack = !this.filter.attack || pokemon.attack >= this.filter.attack;
        const hasDefense = !this.filter.defense || pokemon.defense >= this.filter.defense;
        return hasName && hasType && hasAttack && hasDefense;
      });
    },
    sorted() {
      const field = this.sort.field;
      const direction = this.sort.direction;
      return this.filtered.slice().sort((a, b) => {
        if(a[field] > b[field]) {
          return 1 * direction;
        }
        if(a[field] < b[field]) {
          return -1 * direction;
        }
        return 0;
      });
    }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>