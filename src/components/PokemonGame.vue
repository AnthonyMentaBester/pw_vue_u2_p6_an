<template>
  <div>
    <div class="game-container">
      <button v-on:click="jugar" :disabled="isButtonDisabled()">Jugar</button>
      <div class="images-container">
        <div v-for="(pokemon, index) in pokemons" :key="index" class="pokemon-container">
          <img :src="pokemon.img" alt="pokemon" v-if="pokemon.img">
          <p>{{ pokemon.name }}</p>
        </div>
      </div>
      <div class="status">
        <p>Puntaje: {{ puntos }}</p>
        <p>Intentos restantes: {{ intentos }}</p>
      </div>
      <div v-if="isGameOver()" class="message red">
        <p>Haz utilizado tus 5 intentos</p>
        <p>El juego ha terminado, intentalo nuevamente</p>
      </div>
      <div v-if="isGameWon()" class="message blue">
        <p>Puntaje: {{ puntos }}</p>
        <p>Felicitaciones has ganado un premio de $10,000.00</p>
        <img src="./assets/congratulations.gif" alt="Congratulations">
      </div>
      <button @click="nuevoJuego" v-if="isGameOver() || isGameWon()">Nuevo Juego</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemons: Array(3).fill({ img: null, name: 'X' }),
      puntos: 0,
      intentos: 5,
    };
  },
  methods: {
    async jugar() {
      if (this.intentos === 0 || this.puntos >= 10) return;

      const ids = this.obtenerPokemonIds();
      const promises = ids.map(id => fetch(`https://pokeapi.co/api/v2/pokemon/${id}`).then(res => res.json()));

      const pokemonsData = await Promise.all(promises);

      this.pokemons = pokemonsData.map(pokemon => ({
        img: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${pokemon.id}.svg`,
        name: pokemon.name,
      }));

      this.calcularPuntaje();
      this.intentos -= 1;
    },
    obtenerPokemonIds() {
      const ids = [1, 2, 3, 4, 5];
      return Array(3).fill(null).map(() => ids[Math.floor(Math.random() * ids.length)]);
    },
    calcularPuntaje() {
      const nombres = this.pokemons.map(pokemon => pokemon.name);
      const uniqueNombres = [...new Set(nombres)];

      if (uniqueNombres.length === 1) {
        this.puntos += 5;
      } else if (uniqueNombres.length === 2) {
        this.puntos += 2;
      }
    },
    nuevoJuego() {
      this.puntos = 0;
      this.intentos = 5;
      this.pokemons = Array(3).fill({ img: null, name: 'X' });
    },
    isButtonDisabled() {
      return this.intentos === 0 || this.puntos >= 10;
    },
    isGameOver() {
      return this.intentos === 0 && this.puntos < 10;
    },
    isGameWon() {
      return this.puntos >= 10;
    },
  },
};
</script>


<style>
.game-container {
  text-align: center;
}
.images-container {
  display: flex;
  justify-content: center;
}
.pokemon-container {
  margin: 0 10px;
}
.status, .message {
  margin-top: 20px;
}
.message.red {
  color: red;
}
.message.blue {
  color: blue;
}
button {
  margin-top: 20px;
}
</style>
