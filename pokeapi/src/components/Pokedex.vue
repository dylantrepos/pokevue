<template>
  <div class="container">
    <div class="aside">
      <div class="left-bloc-top">
        <div class="circle-left"></div>
        <div class="circle circle-red"></div>
        <div class="circle circle-yellow"></div>
        <div class="circle circle-green"></div>
      </div>
      <div class="left-bloc-bottom">
        <div class="left-layout-3"></div>
        <div class="left-layout-2"></div>
        <div class="left-layout-1"></div>
      </div>
      
    </div>
    <div class="aside">
  <!-- Content -->
    </div>
  </div>
  
</template>

<script>
import PokemonEvolutions from './pokemon/PokemonEvolutions/PokemonEvolutions.vue';
import PokemonImage from './pokemon/PokemonImage/PokemonImage.vue';
import PokemonSearch from './pokemon/PokemonSearch/PokemonSearch.vue';

  export default {
  components: { PokemonImage, PokemonEvolutions, PokemonSearch },
    data() {
      return {
        url: 'https://pokeapi.co/api/v2/pokemon',
        pokemon: null,
        lastPokemon: 'pikachu',
        error: false,
      }
    },
    methods: {
      async callPokemon(lastPokemon) {
        this.lastPokemon = lastPokemon;
        try {
          this.error = false;
          if(this.pokemon?.name !== this.lastPokemon){  
            this.pokemon = await fetch(`${this.url}/${this.lastPokemon}`).then((data) => data.json());
            console.log('ici')
          }
        } catch(error) {
          this.error = true;
        }
      },
    },
  }
</script>

<style scoped lang="scss">

</style>
