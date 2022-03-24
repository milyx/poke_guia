<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <img src="./assets/poke.png" alt="logo" class="img" />
          <h1 class="py-3">PokeGuía</h1>
        </div>
        <div class="col-12">
          <span>Nombre: </span><input type="text" v-model="pokeIngresado" />
          <button class="mx-2" @click="captarPoke">Buscar</button>
        </div>
        <div class="col-12">
          <h1 class="py-3">{{ nombrepokemon }}</h1>
          <img :src="pokemonfind.imagen" alt="" />
          <h2>Movimientos</h2>
          <p v-for="(item, i) in pokemonfind.moves" :key="i">
            {{ item.move.name }}
          </p>
          <h2>Habilidades</h2>
          <p v-for="(item, i) in pokemonfind.abilities" :key="i">
            {{ item.ability.name }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      url: "https://pokeapi.co/api/v2/pokemon/",
      pokeIngresado: "pikachu",
      pokemonfind: {},
    };
  },
  created() {
    this.captarPoke();
  },

  computed: {
    nombrepokemon() {
      return this.pokemonfind.name + "Poke";
    },
  },
  methods: {
    captarPoke() {
      try {
        fetch(this.url + this.pokeIngresado)
          .then((response) => response.json())
          .then((data) => {
            this.pokemonfind = {
              abilities: data.abilities,
              moves: data.moves,
              imagen: data.sprites?.other?.dream_world?.front_default,
              name: data.name,
            };
          });
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.img {
  width: 300px;
  padding-bottom: 40px;
}
</style>
