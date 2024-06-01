<template>
  <v-app>
    <v-main >
      <div>
        <h1 class="d-flex justify-center align-center ma-5">Pokedex</h1>
        <v-responsive class="mx-auto" max-width="344">
          <v-text-field label="Buscar Pokemon" placeholder="Digite o nome do pokemon" type="text" v-model="pokemonName"></v-text-field>
          <v-btn color="success" class="mb-5" block @click="SearchPokemon">Buscar</v-btn>
        </v-responsive>
       
      </div>
      <v-card class="mx-auto" max-width="300">
        <v-list>
          <v-list-item v-for="(pokemon, index) in pokeListOrder" :key="pokemon">
            <Pokemon :name="pokemon.name" :url="pokemon.url" :num="index" />
          </v-list-item>
        </v-list>
      </v-card>

    </v-main>
  </v-app>
</template>

<script>
//Axios é uma das principais bibliotecas para fazer requisição http
import axios from "axios";
import Pokemon from "./components/Pokemon.vue"



export default {
  name: 'App',

  components: {
    Pokemon,
  },

  created() {

    this.PokemonList();

  },


  methods: {
    PokemonList() {
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0.").then(response => {
        var unOrderList = response.data.results;
        this.pokeListOrder = unOrderList;
      }).catch(error => {
        console.log(error)
      })
    },

    SearchPokemon(){
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0.").then(response => {
        var search = response.data.results;
        if(this.pokeListOrder == "" || this.pokeListOrder == " "){
          this.pokeListOrder = search
        }else{
        this.pokeListOrder = search.filter(pokemon => pokemon.name.toLowerCase() === this.pokemonName.toLowerCase());
      }}).catch(error => {
        console.log(error)
      })
    }
    
  },

  data: () => ({

    pokeListOrder: [],
    pokemonName:""


  }),
}
</script>
