<template>
  <header class="header">
    <a href="/" class="logo">
      <img src="/images/Pokédex_logo.png" alt="Logo Pokedex">
    </a>
    <label for="pokemonInput">
      <form>
        <div class="form-group">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="icon-search">
            <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
          </svg> 
          <input
          type="text"
          id="pokemonInput"
          name="pokemonInput"
          v-model="pokemonID"
          placeholder="Buscar ID o Nombre de pokemon">
        </div>
      </form>    
    </label>
    <button class="searchButton" @click="searchPokemon">Buscar</button>
  </header>

  <main
    class="main"
    v-if="Object.entries(pokemonData).length > 0">
    
    <section class="pokemonCard">
      <div class="nameImage">
        <h1 class="pokemonName">{{ pokemonData.name }}</h1>
        <img
          :src="pokemonData.sprites.front_default"
          :alt="pokemonData.name">
        <h2 class="pokemonID"># {{ pokemonData.id }}</h2>
      </div>
      <ul class="type">
        <h2>Type:</h2>
        <li
          v-for="(type, key) in pokemonData.types"
          :key="key"
          :class="type.type.name"
        >
          <span>{{ type.type.name }}</span>
        </li>
      </ul>
      <ul class="stats">
        <h2>Stats:</h2>
        <li
          v-for="(stat, key) in pokemonData.stats"
          :key="key"
        >
          <span>{{ stat.stat.name}} -> {{stat.base_stat }}</span>
        </li>
      </ul>
    </section>
  </main>
  <header class="container"> 
  </header>
  <main class="card-list-pokemon container">
        <a href="/" class="card-pokemon">
            <div class="card-img">
                <img src="https://assets.pokemon.com/assets/cms2/img/pokedex/detail/001.png" alt="Pokemon bulbasaur">
            </div>
            <div class="card-info">
                <span class="pokemon-id">N° 01
                    <h3>Bulbasaur</h3>
                    <div class="card-types">
                        <span class="grass">Planta</span>
                        <span class="poison">Veneno</span>
                    </div>
                </span>
            </div>

        </a>
        <a href="" class="card-pokemon">
            <div class="card-img">
                <img src="https://assets.pokemon.com/assets/cms2/img/pokedex/detail/002.png" alt="Pokemon Ivysaur">
            </div>
            <div class="card-info">
                <span class="pokemon-id">N° 02
                    <h3>Ivysaur</h3>
                    <div class="card-types">
                        <span class="grass">Planta</span>
                        <span class="poison">Veneno</span>
                    </div>
                </span>
            </div>

        </a>

        <a href="" class="card-pokemon">
            <div class="card-img">
                <img src="https://assets.pokemon.com/assets/cms2/img/pokedex/detail/003.png" alt="Pokemon Venusaur">
            </div>
            <div class="card-info">
                <span class="pokemon-id">N° 03
                    <h3>Venusaur</h3>
                    <div class="card-types">
                        <span class="grass">Planta</span>
                        <span class="poison">Veneno</span>
                    </div>
                </span>
            </div>

        </a>
        </main>
        
</template>

<script>
import { pokeapi } from '@/api/pokeapi'

export default {
  name: 'App',
  data () {
    return {
      pokemonData: {},
      pokemonName: '',
    }
  },

  methods: {
    async searchPokemon () {
      try {
        const pokemonToFind = await fetch(`${pokeapi}/${this.pokemonID}`)
        const pokemon = await pokemonToFind.json()
        this.pokemonData = pokemon
        console.log(pokemon)
        return pokemon
      } catch (error) {
        alert('Pokemon was not found')
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import './pokemon_types.scss';
</style>