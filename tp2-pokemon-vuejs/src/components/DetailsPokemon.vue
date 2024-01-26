<template>
    <div class="container">
        <div class="header">
            <h2>{{ pokemon.name }}</h2>
            <img :src="pokemon.image" :alt="pokemon.name" />
            <div class="stats">
                <p>HP: {{ pokemon.stats.HP }}</p>
                <p>Attack: {{ pokemon.stats.attack }}</p>
                <p>Defense: {{ pokemon.stats.defense }}</p>
                <p>Special Attack: {{ pokemon.stats.special_attack }}</p>
                <p>Special Defense: {{ pokemon.stats.special_defense }}</p>
                <p>Speed: {{ pokemon.stats.speed }}</p>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios';

export default {
    name: "DetailsPokemon",
    data() {
        return {
            pokemon: {}
        }
    },
    created() {
        const pokemonId = this.$route.params.id;
        axios.get(`https://pokebuildapi.fr/api/v1/pokemon/${pokemonId}`)
            .then(response => {
                this.pokemon = response.data;
            })
            .catch(error => {
                console.error(error);
            });
    }
}
</script>


<style scoped>
.container {
    display: flex;
    justify-content: center;
    height: 93vh;
    align-items: center;
}

.header {
    width: 340px;
    height: 500px;
    border: 3px solid black;
    border-radius: 10px;
    margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    flex: 0 0 calc(33.33% - 20px);
}

.header h2 {
    text-transform: uppercase;
    font-size: 1.5em;
    color: #333;
}

.header img {
    width: 40%;
    height: 200px;
    object-fit: cover;
    border-radius: 5px;
    margin-bottom: 20px;
}

.stats {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
}

.stats p {
    width: 100%;
    font-size: 1em;
    color: #000;
    text-align: center;
    margin: 4px;
    font-weight: bold;
}
</style>