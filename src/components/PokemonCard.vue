<script>
import axios from 'axios';

export default {
  props: ['pokemon'],
  data() {
    return {
      nombreIngresado: '',
      descubierto: false,
      pokemonImage: ''
    };
  },
  computed: {
    imageStyle() {
      return this.descubierto ? '' : 'filter: blur(5px) grayscale(100%)';
    }
  },
  methods: {
    verificarNombre() {
      if (this.nombreIngresado.toLowerCase() === this.pokemon.name) {
        this.descubierto = true;
        this.$emit('descubrirPokemon');
      } else {
        alert('Nombre incorrecto');
      }
    }
  },
  mounted() {
    axios.get(this.pokemon.url)
      .then(response => {
        this.pokemonImage = response.data.sprites.front_default;
      });
  }
};
</script>

<template>
  <div class="card p-3 text-center">
    <img :src="pokemonImage" :style="imageStyle" alt="pokemon" class="pokemon-img mb-2" />

    <input v-if="!descubierto" v-model="nombreIngresado" @keyup.enter="verificarNombre" class="form-control mb-2"
      placeholder="Adivina el nombre" />
    <div v-if="!descubierto" class="d-flex justify-content-center">
      <button @click="verificarNombre" class="btn pokemon-btn">Descubrir</button>
    </div>
    <p v-if="descubierto">{{ pokemon.name }}</p>
  </div>
</template>

<style scoped>
.pokemon-img {
  display: block;
  margin: 0 auto;
  width: 100%;
  height: auto;
}

.pokemon-btn {
  background: linear-gradient(45deg, #ebde69, #6681b9, #f17c7c);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  font-size: 16px;
  font-weight: bolder;
  margin-top: 10px;
}

.pokemon-btn:hover {
  background: linear-gradient(45deg, #ff0000, #3b4cca, #ffcc00);
}

.card {
  border: 1px solid #ccc;
  border-radius: 10px;
  margin-top: 20px;
}
</style>
