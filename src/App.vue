<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokebola.jpg" alt="" height="90px" width="90px" />
      <h4 class="is-size-4">Pokedex</h4>
      <input
        type="text"
        class="input is-danger"
        name=""
        id=""
        placeholder="Digite um nome"
        v-model="search"
      />
      <button class="button is-danger" id="search" @click="resultSearch">Search</button>
      <div v-for="(poke, index) in filterdPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filterdPokemons: [],
      search: "",
    };
  },
  created: function() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filterdPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    resultSearch: function() {
      this.filterdPokemons = this.pokemons;
      if (this.search == "" || this.search == " ") {
        this.filterdPokemons = this.pokemons;
      } else {
        this.filterdPokemons = this.pokemons.filter(pokemon => pokemon.name == this.search);
      }
    },
  },
  computed: {
    // resultSearch: function() {
    //   if (this.search == "" || this.search == " ") {
    //     return this.pokemons
    //   } else {
    //     return this.pokemons.filter(pokemon => pokemon.name == this.search);
    //   }
    // }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#search {
  margin-top: 5px;
}
</style>
