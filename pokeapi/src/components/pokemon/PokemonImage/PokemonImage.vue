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
            imageshow: null,
            pokemonImage: null,
        }
    },
    methods: {
      animationImg() {
          if(this.pokemonImage.back_default) {
            if(this.imageshow === this.pokemonImage.front_default) {
              this.imageshow = this.pokemonImage.back_default;
              this.$refs.imgFront.classList.remove('anim-img-enter');
              this.$refs.imgBack.classList.add('anim-img-enter');
            }
            else {
              this.imageshow = this.pokemonImage.front_default;
              if(this.$refs.imgBack) this.$refs.imgBack.classList.remove('anim-img-enter');
              this.$refs.imgFront.classList.add('anim-img-enter');
            }
          } 
      },
      async initFirstImage() {
        this.imageshow = this.pokemonImage?.front_default;
        this.$refs.imgBack?.classList.remove('anim-img-enter');
        this.$refs.imgFront?.classList.add('anim-img-enter');
      }
    },
    mounted() {
        this.initFirstImage()    
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
