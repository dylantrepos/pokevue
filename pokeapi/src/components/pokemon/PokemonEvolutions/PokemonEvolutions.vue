<template>
  <div  class="box_evo">
     <div class="box_evo-images-all">
        <PokemonEvolutionImage
            v-for="pokemon of pokemonEvolutions" :pokemon="pokemon" 
            @click="$emit('newName', pokemon?.name)" 
        />
     </div>
     <p v-show="pokemonEvolutions.length < 1">No evolution for this pokemon.</p>
  </div>
</template>

<script>
import PokemonEvolutionImage from './PokemonEvolutionImage/PokemonEvolutionImage.vue';

  export default {
  components: { PokemonEvolutionImage },
    props: ['pokemon'],
    data() {
      return {
        url: 'https://pokeapi.co/api/v2/pokemon',
        pokemonName: 'pikachu',
        pokemonEvolutions: [],
        error: false,
      }
    },
    methods: {
      async callPokemon() {
        try {
            this.error = false;
            this.pokemonEvolutionLink = await fetch(this.pokemon?.species.url).then((data) => (data.json()))
            this.pokemonEvolutionData = await fetch(this.pokemonEvolutionLink.evolution_chain.url).then((data) => (data.json()))
            let path = this.pokemonEvolutionData.chain;
            this.pokemonEvolutions = [];
            this.pokemonEvolutions.push(fetch(`${this.url}/${path.species.name}`).then((data) => data.json()))

            while(path.evolves_to[0]) {
                for(const evolution of path.evolves_to){
                    this.pokemonEvolutions.push(fetch(`${this.url}/${evolution.species.name}`).then((data) => data.json()))
                }
                path = path.evolves_to[0];
            } 

            this.pokemonEvolutions = await Promise.all(this.pokemonEvolutions)
            this.pokemonEvolutions = this.pokemonEvolutions.filter((pokemonEvo) => pokemonEvo.name !== this.pokemon.name)
        } catch(error) {
          this.error = true;
        }
      },
    },
    mounted() {

    },
    watch: {
        pokemon: function() {
            this.callPokemon();
        }
    }
  }
</script>

<style scoped lang="scss">
@import './PokemonEvolutions.scss';
</style>
