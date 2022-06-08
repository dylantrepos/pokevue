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
                <div class="middle-element"></div>
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
                   <button class="btn-search" type="submit">
                    <img src="../assets/pokeball.svg" alt="">
                    <p>SEARCH</p>
                  </button>
                  <button class="btn-random">
                    <img src="../assets/pokeball.svg" alt="">
                    <p>RANDOM</p>
                  </button>
              </div>
              <div class="control-bottom-layout">
                  <form action="" class="search-bar">
                    <input type="text" value="Pikachu">
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
    <div class="aside -right">
      <div class="right-bloc">
        <div class="right-layout-3"></div>
        <div class="right-layout-2"></div>
        <div class="right-layout-1"></div>
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
