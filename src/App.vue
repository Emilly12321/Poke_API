<template>
  <div id="App " class="has-background-white-ter">
    <div class="column is-4 is-offset-4">

      <div v-for="(poke, index) in pokemons" :key="index">

        <Pokemons :name="poke.name" :url="poke.url" :num="index + 1" />

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
    }
  },
  created: function () {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      console.log(this.pokemons)
    })

  },
  components: {
    Pokemons
  }
}


</script>

<style scoped></style>
