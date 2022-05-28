<template>
  <h1 class="pokemon-name">{{ pokemon?.name }}</h1>
  <h5>Type : {{this.pokemon?.types[0].type.name}}</h5>
  <PokemonImage :pokemon="pokemon" />
  <PokemonSearch :pokemon="pokemon" @change-pokemon="callPokemon"/>
  <p v-if="error">Sorry, this pokemon doesn't exists.</p>
  <PokemonEvolutions :pokemon="pokemon" @change-pokemon="callPokemon" :url="url" />
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
