<template>
  <div class="wrapper-container flex">
    <PokemonBanner></PokemonBanner>
    <div class="random-pokemon flex">
      <div v-if="isPokemongenerated">
        <h2>{{ pokemon.name }}</h2>
        <img class="pokemon" :src="pokemon.img" alt="Generated Pokemon" />
      </div>
    </div>
    <img
      class="pokeball"
      src="@/assets/images/pokeball.png"
      alt="pokeball"
      @click="getRandomPokemon()"
    />
    <p><em>Click to the Pokéball to generate</em></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isPokemongenerated: false,
      pokemon: {
        name: '',
        img: '',
      },
    }
  },
  methods: {
    getRandomNumber() {
      return Math.floor(Math.random() * 200) + 1
    },
    getRandomPokemon() {
      const url =
        process.env.API_PROTOCOL +
        process.env.API_URL +
        process.env.API_VERSION +
        process.env.API_ENDPOINT +
        this.getRandomNumber()
      fetch(url)
        .then((data) => data.json())
        .then((pokemon) => {
          this.isPokemongenerated = true
          this.pokemon.name = pokemon.name
          this.pokemon.img = pokemon.sprites.front_default
        })
        .catch((err) => {
          console.error(err)
        })
    },
  },
}
</script>

<style>
.flex {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.wrapper-container {
  height: 100vh;
}

.pokemon-banner {
  height: 10vh;
}

.random-pokemon {
  border-radius: 1rem;
  border: 1rem solid #3366af;
  height: 300px;
  margin: 3rem 0;
  width: 300px;
}
.random-pokemon > div {
  width: 100%;
}
.random-pokemon h2 {
  text-align: center;
  font-size: 2rem;
}
.random-pokemon img {
  display: block;
  margin: 0 auto;
  height: 100%;
}

.pokeball {
  cursor: pointer;
  height: 5vh;
}

p {
  margin-top: 2rem;
}
</style>
