<template>
  <div class="box-image">
      <img 
        :src="this.pokemonImage?.front_default" 
        class="img-result img-front"
        ref="imgFront"
      >
      <img 
        :src="this.pokemonImage?.back_default ?? this.pokemonImage?.front_default" 
        class="img-result img-back"
        ref="imgBack"
      >
  </div>
</template>

<script>

  export default {
    props: ['pokemon'],
    data() {
        return {
            pokemonImage: null,
            myInterval: null,
            test: null,
            test2: null,
        }
    },
    methods: {
      animationImg() {
        if(this.pokemonImage) {
            this.$refs.imgFront?.classList.toggle('anim-img-enter')
            this.$refs.imgBack?.classList.toggle('anim-img-enter');
        } 
      },
      async initFirstImage() {
        this.$refs.imgBack?.classList.add('anim-img-enter');
        this.$refs.imgFront?.classList.remove('anim-img-enter');
      }
    },
    watch: { 
      	pokemon: async function() { 
          this.pokemonImage = await this.pokemon?.sprites;
          this.initFirstImage()
          this.myInterval ? clearInterval(this.myInterval) : ''
          this.animationImg();
          this.myInterval = setInterval(this.animationImg, 3000)
        }
    },
  }
</script>

<style scoped lang="scss">
@import './PokemonImage.scss';
</style>
