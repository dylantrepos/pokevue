<template>
  <div class="box-searchPokemon">
    <form @submit.prevent="callPokemon">
      <input v-model="pokemonName">
      <div class="box-button-searchbox">
        <button>
          <img src="../../../assets/pokeball.svg" alt="">
          <p>SEARCH</p>
        </button>
        <button @click="generatePokemon">
          <img src="../../../assets/pokeball.svg" alt="">
          <p>RANDOM</p>
        </button>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
      props: ['pokemonName'],
    data() {
      return {
        url: 'https://pokeapi.co/api/v2/pokemon',
        pokemon: null,
        pokemonName: 'pikachu',
        listPokeNames: [],
        error: false,
      }
    },
    computed: {
    },
    methods: {
      async callPokemon() {
        try {
          this.error = false;
          if(this.pokemon?.name !== this.pokemonName){  
            this.pokemon = await fetch(`${this.url}/${this.pokemonName}`).then((data) => data.json());
          }
        } catch(error) {
          this.error = true;
        }
      },
      generatePokemon() {
        const randomR = Math.floor(Math.random() * (0 - 1126 + 1) + 1126);
        this.pokemonName = this.listPokeNames[randomR]?.name
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
</style>
