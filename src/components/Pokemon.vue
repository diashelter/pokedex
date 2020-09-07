<template>
  <div class="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} {{ name | upper }}</p>
            <p class="subtitle is-6">
              {{ pokemon.type }}
            </p>
            <p class="subtitle is-6">
              {{ pokemon.abilities }}
            </p>
          </div>
        </div>
        <div class="content">
          <button class="button is-primary is-rounded" @click="changeImg">Mudar imagem</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function() {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.abilities = res.data.abilities[0].ability.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.pokemon.stats = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        typeOne: "",
        front: "",
        back: "",
        abilitiesOne: "",
        stats: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: function(value) {
      let newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods: {
    changeImg: function() {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
          this.isFront = true;
          this.currentImg = this.pokemon.front;
      }
    },
  },
};
</script>

<style>
.pokemon {
  margin: 5px auto;
}
</style>
