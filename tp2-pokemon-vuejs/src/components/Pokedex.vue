<template>
    <div>
        <router-view></router-view>
        <TypeCounts :pokemons="Tableaupokemon" />
        <h1>Nombre de Pokémon :</h1>
        <input id="input" type="number" v-model="pokemonLimit" @change="fetchPokemons">
        <select v-model="selectedGeneration" @change="fetchGenerationPokemons">
            <option v-for="gen in 8" :key="gen" :value="gen">
                {{ 'Generation ' + gen }}
            </option>
        </select>
        <div class="Pokedex">
            <div v-for="pokemon, _ in Tableaupokemon" :key="pokemon.id">
                <router-link :to="`/pokemon/${pokemon.id}`" target="_blank">
                    <Pokemon :infoPokemon="pokemon" />
                </router-link>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios';
import Pokemon from './Pokemon.vue'
import TypeCounts from './TypeCounts.vue'

export default {
    name: "Pokedex",
    props: ['infoPokemon'],
    components: {
        Pokemon,
        TypeCounts
    },
    data() {
        return {
            Tableaupokemon: [],
            pokemonLimit: 20,
            selectedGeneration: 1
        }
    },
    methods: {
        fetchPokemons() {
            axios.get(`https://pokebuildapi.fr/api/v1/pokemon/limit/${this.pokemonLimit}`)
                .then(response => {
                    this.Tableaupokemon = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        fetchGenerationPokemons() {
            axios.get(`https://pokebuildapi.fr/api/v1/pokemon/generation/${this.selectedGeneration}`)
                .then(response => {
                    this.Tableaupokemon = response.data.slice(0, this.pokemonLimit);
                })
                .catch(error => {
                    console.error(error);
                });
        }
    },
    mounted() {
        this.fetchPokemons();
    }
};
</script>

<style>
.Pokedex {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 20px;
}

h1 {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 20px;
}

.pokemon-item {
    margin-bottom: 20px;
}

#input {
    width: 99%;
    height: 50px;
    border: 3px solid black;
    border-radius: 10px;
    padding: 20px;
    margin: 10px;
    display: flex;
    background-color: #bdbdbd;
    font-size: 16px;
}

select {
    padding: 10px;
    border: none;
    border-radius: 5px;
    border: 3px solid black;
    border-radius: 10px;
    padding: 20px;
    margin: 10px;
    background: #bdbdbd;
    font-size: 16px;
    outline: none;
    width: 99%;
}

select option {
    background: #bdbdbd;
    color: black;
}
</style>