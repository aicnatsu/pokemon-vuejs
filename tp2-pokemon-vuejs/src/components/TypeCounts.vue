<template>
    <h1>Nombre de Pokémons par type : </h1>
    <div class="type-counts">
        <div v-for="(count, type) in getPokemonCountsByType()" :key="type" class="type-count">
            <img :src="getTypeImage(type)" :alt="type" />
            <span>{{ type }} : {{ count }}</span>
        </div>
    </div>
</template>
  
<script>
export default {
    props: {
        pokemons: {
            type: Array,
            required: true
        }
    },
    methods: {
        getPokemonCountsByType() {
            const counts = {};
            this.pokemons.forEach(pokemon => {
                pokemon.apiTypes.forEach(type => {
                    if (counts[type.name]) {
                        counts[type.name]++;
                    } else {
                        counts[type.name] = 1;
                    }
                });
            });
            return counts;
        },
        getTypeImage(type) {
            for (let pokemon of this.pokemons) {
                for (let apiType of pokemon.apiTypes) {
                    if (apiType.name === type) {
                        return apiType.image;
                    }
                }
            }
            return '';
        }
    }
};
</script>

<style scoped>
h1 {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 20px;
}

.type-counts {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    padding: 10px;
    border: 1px solid #000;
    border-radius: 5px;
    background-color: #bdbdbd;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    margin: 10px;
    max-width: 100%;
    overflow: auto;
}

.type-count {
    display: flex;
    align-items: center;
    margin: 10px;
    padding: 10px;
    border: 1px solid #000;
    border-radius: 5px;
    background-color: #FFD880;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.type-count img {
    width: 50px;
    height: 50px;
    margin-right: 10px;
}

.type-count span {
    font-size: 1.2em;
}
</style>