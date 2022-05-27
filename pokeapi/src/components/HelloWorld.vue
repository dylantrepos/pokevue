<template>
  <h1>{{ pokemon?.name }}</h1>
  <div 
    class="box-image">
      <img 
      :src="pokemonImage?.front_default" 
      class="img-result img-front"
      ref="imgFront"
      >
      <img 
      :src="pokemonImage?.back_default" 
      class="img-result img-back"
      ref="imgBack"
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

  export default {
    data() {
      return {
        message: 'Let\'s go !',
        url: 'https://pokeapi.co/api/v2/pokemon',
        pokemon: null,
        pokemonName: 'pikachu',
        pokemonsEvolution: [],
        listPokeNames: [],
        imageShow: null,
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
            this.pokemon = await fetch(`${this.url}/${this.pokemonName}`).then((data) => data.json());
            this.pokemonImage = await this.pokemon.sprites;

            this.imageShow = this.pokemonImage.front_default;
            this.$refs.imgBack.classList.remove('anim-img-enter');
            this.$refs.imgFront.classList.add('anim-img-enter');
            
            const link = this.pokemon.species.url;
            this.pokemonEvolutionLink = await fetch(link).then((data) => (data.json()))
            this.pokemonEvolutionData = await fetch(this.pokemonEvolutionLink.evolution_chain.url).then((data) => (data.json()))
            let path = this.pokemonEvolutionData.chain;
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
      },
      animationImg() {
          if(this.pokemonImage.back_default) {
            if(this.imageShow === this.pokemonImage.front_default) {
              this.imageShow = this.pokemonImage.back_default;
              this.$refs.imgFront.classList.remove('anim-img-enter');
              this.$refs.imgBack.classList.add('anim-img-enter');
            }
            else {
              this.imageShow = this.pokemonImage.front_default;
              if(this.$refs.imgBack) this.$refs.imgBack.classList.remove('anim-img-enter');
              this.$refs.imgFront.classList.add('anim-img-enter');
            }
          } 
      },
      generatePokemon() {
        function randomInRange(min, max)
        {
          return Math.floor(Math.random() * (max - min + 1) + min);
        }
        const randomR = randomInRange(0, 1126);
        const myArr = this.listPokeNames
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
      setInterval(this.animationImg, 3000)
    },
  }
</script>

<style scoped>
h1 {
  color: #42b983;
}
</style>
