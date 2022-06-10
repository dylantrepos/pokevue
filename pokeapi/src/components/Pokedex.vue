<template>
  <div class="container">
    <div class="aside -left">
      <div class="left-bloc-top">
        <div class="circle-left">
          <div class="circle-left-inside"></div>
        </div>
        <div class="circle circle-red"></div>
        <div class="circle circle-yellow"></div>
        <div class="circle circle-green"></div>
      </div>
      <div class="left-layout-4"></div>
      <div class="left-layout-3"></div>
      <div class="left-layout-2"></div>
      <div class="left-layout-1"></div>
      <div class="left-bloc-bottom">
        <div class="left-layout-elements">
            <div class="screen-layout">
              <div class="screen-element">
                <div class="top-element">
                  <div class="red-light-top"></div>
                  <div class="red-light-top"></div>
                </div>
                <div class="middle-element">
                  <PokemonImage :pokemon="pokemon" />
                </div>
                <div class="bottom-element">
                  <div class="red-light-bottom"></div>
                  <div class="lines-layout-bottom">
                    <hr>
                    <hr>
                    <hr>
                    <hr>
                    <hr>
                    <hr>
                    <hr>
                    <hr>
                    <hr>
                    <hr>
                  </div>
                </div>
              </div>
            </div>
            <div class="control-layout">
              <div class="control-top-layout">
                  <div class="round-black"></div>
                   <button class="btn-search" type="submit" @click="callPokemon(pokemonSearch)">
                    <img src="../assets/pokeball.svg" alt="">
                    <p>SEARCH</p>
                  </button>
                  <button class="btn-random" @click="generatePokemon">
                    <img src="../assets/pokeball.svg" alt="">
                    <p>RANDOM</p>
                  </button>
              </div>
              <div class="control-bottom-layout">
                  <form @submit.prevent="callPokemon(pokemonSearch)" class="search-bar">
                    <input type="text"  v-model="pokemonSearch" class="pokemon-name">
                  </form>
                  <div class="cross-layer">
                      <div class="top-cross">
                        <div class="cross cross-vertical"></div>
                      </div>
                      <div class="middle-cross">
                        <div class="cross cross-left"></div>
                        <div class="cross-middle-horizontal"></div>
                        <div class="cross cross-right"></div>
                      </div>
                      <div class="bottom-cross">
                        <div class="cross cross-vertical"></div>
                      </div>
                  </div>
              </div>
            </div>
        </div>
        <div class="left-pivot"></div>
      </div>
      
    </div>
  </div>
  <div class="container -cover_left">
    <div class="aside -left">
      <div class="left-layout-4"></div>
      <div class="left-layout-3"></div>
      <div class="left-layout-2"></div>
      <div class="left-layout-1"></div>
    </div>
    <div class="aside -right">

    </div>
  </div>
  <div class="container -cover_right">
    <div class="aside -left">

    </div>
  <div class="aside -right">
      <div class="right-bloc">
        <div class="right-layout-3"></div>
        <div class="right-layout-2"></div>
        <div class="right-layout-1">
        </div>
        <div class="right-bloc-bottom">
        <div class="right-layout-elements">
          <div class="right-layout-top">
            <div class="right-layout-top-box">
              <div class="screen-general">
                <div v-if="pokemon?.types">
                  <h1 class="pokemon-name">{{ pokemon?.name }}</h1>
                  <h5>Type : {{pokemon?.types[0].type.name}}</h5>
                </div>
              </div>
              <div class="screen-general2"></div>
            </div>
          </div>
          <div class="right-layout-middle"></div>
          <div class="right-layout-bottom"></div>
        </div>
      </div>
      </div>
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
        pokemonSearch: 'pikachu',
        lastPokemon: '',
        listPokeNames: [],
        error: false,
      }
    },
    methods: {
      async callPokemon(pokemonSearch = this.pokemonSearch) {
        try {
          this.error = false;
          if(pokemonSearch !== this.lastPokemon){  
            this.pokemon = await fetch(`${this.url}/${pokemonSearch}`).then((data) => data.json());
            this.lastPokemon = this.pokemonSearch;
            this.pokemonSearch = pokemonSearch;
          }

        } catch(error) {
          this.error = true;
        }
      },
      generatePokemon() {
        const randomR = Math.floor(Math.random() * (0 - 1126 + 1) + 1126);
        this.pokemon = this.listPokeNames[randomR]?.name;
        this.callPokemon(this.pokemon);
      },
      test()
      {
        console.log('este')
      }
    },
    async mounted() {
      let data = await fetch(`${this.url}/?offset=20&limit=1126`).then((data) => data.json())
      this.listPokeNames = data.results;
      this.callPokemon(this.pokemonSearch);
    },
  }
</script>

<style scoped lang="scss">

</style>
