<template>
  <div id="App " class="has-background-white-ter">
    <div class="is-flex is-justify-content-center ">
      <img src="./assets/859e0396b1c628832ba6b7c47c4a95b5-removebg-preview.png">
    </div>

    <div class="is-flex is-flex-direction-column is-align-items-center is-gap-2">
      <h1 class="has-text-dark titulo">POKEDEX</h1>
      <div class="field is-flex is-flex-direction-column is-gap-1">
        <p class="control has-icons-right">
          <input class="input input_busca is-small is-rounded" type="text" v-model="busca"
            placeholder="Buscar um pokemon" />
          <!-- <span class="icon icone is-small is-right is-light">
            <i class="fas icons fa-search"></i>
          </span> -->
        </p>
        <button class="button botao is-small  is-rounded " @click="buscarPokemon">Pesquisar</button>
      </div>
    </div>
    <div class="column is-4 is-offset-4">

      <div v-for="(poke,index) in pokemonsFiltrados" :key="poke.url">

        <Pokemons :name="poke.name" :url="poke.url" :num=" index + 1" />

      </div>

    </div>

  </div>

</template>

<script>
import axios from 'axios';
import Pokemons from './components/Pokemons.vue';

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      pokemonsFiltrados: [],
      busca: '',
    }
  },
  created: function () {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.pokemonsFiltrados = res.data.results;
      console.log(this.pokemons)
    })

  },
  components: {
    Pokemons
  },
  // computed:{
  //   resultadoBuscas: function () {
  //     if(this.busca == '' || this.busca == ' '){
  //       return this.pokemons;
  //     }else{
  //       return this.pokemons.filter(pokemon => pokemon.name == this.busca );
  //     }
  //   }
  // },
  methods: {
    buscarPokemon: function () {
      this.pokemonsFiltrados = this.pokemons;
      if (this.busca == '' || this.busca == ' ') {
        this.pokemonsFiltrados = this.pokemons;
      } else {
        let nome = ''
        nome =  this.busca.toLowerCase();
        this.pokemonsFiltrados = this.pokemons.filter(pokemon => pokemon.name == nome);

      }
    },
    lower: function (pokemon) {
            let nome = pokemon.toLowerCase();
            return nome;
        },
  }
}


</script>

<style scoped>
.input_busca {
  max-width: 350px;
  background: #6150fc;
  border: none;
}

.icons {
  color: #ffffffb0;
}

.botao {
  height: 20px;
  background: #3529a0;
  border: none;
}

/* .icone, input:focus{
  color: #fff !important;
} */

.titulo {
  font-size: 24px;
}
</style>
