<template>
  <div class="box-image">
      <img 
        :src="this.pokemonImage?.front_default" 
        class="img-result img-front"
        ref="imgFront"
      >
      <img 
        :src="this.pokemonImage?.back_default" 
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
        }
    },
    methods: {
      animationImg() {
        if(this.pokemonImage && this.pokemonImage.back_default) {
          this.$refs.imgFront?.classList.toggle('anim-img-enter');
          this.$refs.imgBack?.classList.toggle('anim-img-enter');
        } 
      },
      async initFirstImage() {
        this.$refs.imgBack?.classList.remove('anim-img-enter');
        this.$refs.imgFront?.classList.add('anim-img-enter');
      }
    },
    mounted() {    
        setInterval(this.animationImg, 3000);
    },
    watch: { 
      	pokemon: async function() { 
          this.pokemonImage = await this.pokemon?.sprites;
          this.initFirstImage()
        }
    },
  }
</script>

<style scoped lang="scss">
@import './PokemonImage.scss';
</style>
