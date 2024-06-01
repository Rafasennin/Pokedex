<template>
  <v-container>
    <v-card>
      <v-card-item class="bg-blue d-flex justify-center align-center text-center">
        <v-card-title class="text-black">
          <h1>{{ num + 1 }} {{ capitalizeFirstLetter(name) }}</h1>
        </v-card-title>
        <v-divider class="mt-5 "></v-divider>
        <v-card-subtitle>
          <p>{{ pokemon.type }}</p>
        </v-card-subtitle>
        <v-divider></v-divider>
        <v-card-subtitle>
          <v-img  :src="this.pokemon.isFront ? this.pokemon.front : this.pokemon.back"></v-img>
          <v-img src="../assets/logo.png"></v-img>
        </v-card-subtitle>
        <v-divider></v-divider>
        <v-card-actions class="d-flex justify-center align-center text-center">
          <v-btn class="bg-red" @click="turnPokemon">Turn</v-btn>
        </v-card-actions>
      </v-card-item>
    </v-card>

  </v-container>
</template>
  
<script>
import axios from "axios";

 

export default {

  created() {
    axios.get(this.url).then(res => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
    })
  },


  data() {
    return {
      pokemon: {
        type: '',
        front: "",
        back: '',
        isFront: true,
      },

      tools: {
        switchOn: true,
        logo: "../assets/logo.png",
        rafasennin: "@/assets/rafasennin_logo.png"
      }

    }
  },

  name: "Pokemon_component",

  props: {
    num: Number,
    name: String,
    url: String,
  },

  methods: {
    capitalizeFirstLetter(word) {
      return word.charAt(0).toUpperCase() + word.slice(1);

    },

    turnPokemon() {
      this.pokemon.isFront = !this.pokemon.isFront;
    },
  },
};
</script>
  
