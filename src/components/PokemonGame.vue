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
    <img src="@/assets/pokemon-logo.png" alt="Pokémon Logo" class="pokemon-logo" />

    <h2>¡Adivina el Pokémon!</h2>
    <p>Pokemones descubiertos: {{ pokemonsDescubiertos }}</p>
    <div class="row">
      <div class="col-12 col-md-3" v-for="(pokemon, index) in pokemons" :key="index">
        <pokemon-card :pokemon="pokemon" @descubrirPokemon="descubrirPokemon" />
      </div>
    </div>

  </div>
</template>

<style scoped>
.pokemon-logo {
  display: block;
  margin: 0 auto;
  max-width: 200px;
  height: auto;
}

.row {
  margin: 20px 0;
}

h2 {
  text-align: center;
}

p {
  font-size: 20px;
  text-align: center;
  font-weight: bold;
}
</style>
