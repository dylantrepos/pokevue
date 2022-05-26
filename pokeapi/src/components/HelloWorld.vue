<template>
  <h1>{{ pokemon?.name }}</h1>
  <div @mouseover="pokemonImage = pokemon?.sprites?.back_default" @mouseleave="pokemonImage = pokemon?.sprites?.front_default">
    <img 
    :src="pokemonImage" 
    alt="" 
    class="img-result"
    
    >
  </div>
  <div class="box-searchPokemon">
    <form @submit.prevent="callPokemon">
      <input v-model="pokemonName">
      <div class="box-button-searchbox">
        <button>
          <img src="../assets/pokeball.svg" alt="">
          <p>SEARCH</p>
        </button>
        <button @click="generatePokemon">
          <img src="../assets/pokeball.svg" alt="">
          <p>RANDOM</p>
        </button>
      </div>
    </form>
  </div>
  <p v-if="error">Sorry, this pokemon doesn't exists.</p>
  <div  class="box-evolution">
    <ul id="groupPokemonsEvolution">
      <li v-for="pokemon of pokemonsEvolution">
        <div @click="switchPokemon(pokemon?.name)">
          <img :src="pokemon?.sprites?.front_default" alt="">
          <p>{{ pokemon.name }}</p>
        </div>
      </li>
     <p v-show="pokemonsEvolution.length < 1">No evolution for this pokemon.</p>
     </ul>
  </div>
</template>

<script>
  import pokemon from 'pokemon'

  export default {
    data() {
      return {
        message: 'Let\'s go !',
        url: 'https://pokeapi.co/api/v2/pokemon',
        pokemon: null,
        pokemonName: 'pikachu',
        pokemonsEvolution: [],
        listPokeNames: [],
        pokemonImage: null,
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
            this.pokemon = await fetch(`${this.url}/${this.pokemonName}`).then((data) => data.json())
            this.pokemonImage = this.pokemon.sprites.front_default
            const link = this.pokemon.species.url;
            this.pokemonEvolutionLink = await fetch(link).then((data) => (data.json()))
            this.pokemonEvolutionData = await fetch(this.pokemonEvolutionLink.evolution_chain.url).then((data) => (data.json()))
            let path = this.pokemonEvolutionData.chain;
            console.log(this.pokemonEvolutionData)
            this.pokemonsEvolution = [];
            this.pokemonsEvolution.push(fetch(`${this.url}/${path.species.name}`).then((data) => data.json()))

            while(path.evolves_to[0]) {
              for(const evolution of path.evolves_to){
                  this.pokemonsEvolution.push(fetch(`${this.url}/${evolution.species.name}`).then((data) => data.json()))
              }
              path = path.evolves_to[0];
            } 

            this.pokemonsEvolution = await Promise.all(this.pokemonsEvolution)

            this.pokemonsEvolution = this.pokemonsEvolution.filter((pokemonEvo) => pokemonEvo.name !== this.pokemonName)
          }
        } catch(error) {
          this.error = true;
        }
        console.log(this.pokemon)
      },
      generatePokemon() {
        function randomInRange(min, max)
        {
          return Math.floor(Math.random() * (max - min + 1) + min);
        }
        const randomR = randomInRange(0, 1126);
        console.log('r :', randomR)
        const myArr = this.listPokeNames
        console.log('ici : ', this.listPokeNames[0])
        this.pokemonName = this.listPokeNames[randomR].name
      },
      switchPokemon(newPokemon) {
        this.pokemonName = newPokemon;
        this.callPokemon();
      }
    },
    mounted() {
      this.callPokemon();
      const test = async () => {
          let i = 0
          let list = [];
          let data = await fetch(`${this.url}/?offset=20&limit=1126`).then((data) => data.json())
          this.listPokeNames = data.results;
      }
      test()
    },
  }
</script>

<style scoped>
h1 {
  color: #42b983;
}
</style>
