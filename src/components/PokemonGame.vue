<script>
import axios from 'axios';
import PokemonCard from './PokemonCard.vue';

export default {
  data() {
    return {
      pokemons: [],
      pokemonsDescubiertos: 0
    };
  },
  components: {
    PokemonCard
  },
  methods: {
    descubrirPokemon() {
      this.pokemonsDescubiertos++;
    }
  },
  mounted() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=20')
      .then(response => {
        this.pokemons = response.data.results;
      })
      .catch(error => {
        console.error(error);
      });
  }
};
</script>

<template>
  <div>
    <h1>¡Adivina el Pokémon!</h1>
    <div class="row">
      <div class="col-12 col-md-3" v-for="(pokemon, index) in pokemons" :key="index">
        <pokemon-card :pokemon="pokemon" @descubrirPokemon="descubrirPokemon" />
      </div>
    </div>
    <p>Pokemones descubiertos: {{ pokemonsDescubiertos }}</p>
  </div>
</template>



<style scoped>
.row {
  margin: 20px 0;
}

h1 {
  text-align: center;
}
</style>
