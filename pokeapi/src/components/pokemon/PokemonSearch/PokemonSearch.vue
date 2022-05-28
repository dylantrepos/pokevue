<template>
    <form @submit.prevent="callPokemon" class="box-searchPokemon">
      <input v-model="pokemonName">
      <div class="box-button-searchbox">
        <button type="submit">
          <img src="../../../assets/pokeball.svg" alt="">
          <p>SEARCH</p>
        </button>
        <button @click="generatePokemon">
          <img src="../../../assets/pokeball.svg" alt="">
          <p>RANDOM</p>
        </button>
      </div>
    </form>
</template>

<script>
  export default {
    props: ['url'],
    data() {
      return {
        url: 'https://pokeapi.co/api/v2/pokemon',
        pokemonName: 'pikachu',
        listPokeNames: [],
        error: false,
      }
    },
    methods: {
      async callPokemon() {
          this.$emit('change-pokemon', this.pokemonName);
      },
      generatePokemon() {
        const randomR = Math.floor(Math.random() * (0 - 1126 + 1) + 1126);
        this.pokemonName = this.listPokeNames[randomR]?.name;
        this.callPokemon();
      },
    },
    async mounted() {
      let data = await fetch(`${this.url}/?offset=20&limit=1126`).then((data) => data.json())
      this.listPokeNames = data.results;
      this.callPokemon();
    },
  }
</script>

<style scoped lang="scss">
@import './PokemonSearch.scss';
</style>
