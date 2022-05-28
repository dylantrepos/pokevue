<template>
    <div class="box_evo-image-elt">
        <img :src="pokemon?.sprites?.front_default" alt="">
        <p class="pokemon-name">{{ pokemon.name }}</p>
    </div>
</template>

<script>
  export default {
    props: ['pokemon'],
  }
</script>

<style scoped lang="scss">
@import './PokemonEvolutionImage.scss';
</style>
