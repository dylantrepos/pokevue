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
                  <div class="loading-container">
                    <div class="lds-ellipsis" v-if="isLoading">
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                    </div>
                  </div>
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
              <div class="loading-container">
                    <div class="lds-ellipsis" v-if="isLoading">
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                    </div>
                  </div>
              <div class="screen-general">
                <div v-if="pokemon?.types" class="info_general">
                  <h1 class="pokemon-name">{{ pokemon?.name }}</h1>
                  <h5 class="pokemon-type">Type : {{pokemon?.types[0].type.name}}</h5>
                  <p class="pokemon-description">
                    {{ pokemon?.description?.flavor_text?.toLowerCase() ?? 'No description available for this pokemon...' }}
                  </p>
                </div>
              </div>
              <div class="screen-general2"></div>
            </div>
          </div>
          <div class="right-layout-middle">
            <div class="control-btn control-btn-general">
              <img src="../assets/pokeball.svg" alt="">
                <p>Stats</p>
              </div>
            <div class="control-btn control-btn-general">
              <img src="../assets/pokeball.svg" alt="">
                <p>Evolutions</p>
              </div>
            <div class="control-btn control-btn-general">
              <img src="../assets/pokeball.svg" alt="">
                <p>Other</p>
              </div>
            <div class="control-btn control-btn-general">
              <img src="../assets/pokeball.svg" alt="">
                <p>Other</p>
              </div>
            <div class="control-btn control-btn-general">
              <img src="../assets/pokeball.svg" alt="">
                <p>Other</p>
              </div>
            <div class="control-btn control-btn-general">
              <img src="../assets/pokeball.svg" alt="">
                <p>Other</p>
              </div>
          </div>
          <div class="right-layout-bottom">
            <div class="right-layout-top-box">
              <div class="loading-container">
                    <div class="lds-ellipsis" v-if="isLoading">
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                      <div><img src="../assets/pokeball.svg" alt=""></div>
                    </div>
                  </div>
              <div class="screen-general">
                  <div v-if="pokemon?.types" class="info_general">
                    <div class="stats_container">
                      <div v-for="stats in pokemon?.stats" :key="stats.stat.name" class="stats_item">
                        <span>{{stats.stat.name}}</span>
                        <span>{{stats.base_stat}}</span>
                      </div>
                    </div>
                  </div>
                </div>
              <div class="screen-general2"></div>
            </div>
          </div>
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
        isLoading: true,
      }
    },
    methods: {
      async callPokemon(pokemonSearch = this.pokemonSearch) {
        this.isLoading = true;
        try {
          this.error = false;
          if(pokemonSearch !== this.lastPokemon){  
            this.pokemon = await fetch(`${this.url}/${pokemonSearch}`).then(async(data) =>{
              const poke = await data.json();
              let evol = await fetch(`https://pokeapi.co/api/v2/pokemon-species/${poke.id}/`)
                .then(async (data) => {
                  let description = await data.json()
                  description = description.flavor_text_entries.filter((evo) => evo.language.name === 'en')[0]
                  console.log(description)
                  return description;
                  })
                .catch(err => 'No description')
              console.log(evol)
              this.isLoading = false;
              return { ...poke, description: {...evol}}
              });
            this.lastPokemon = this.pokemonSearch;
            this.pokemonSearch = pokemonSearch;
            console.log(this.pokemon)
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
