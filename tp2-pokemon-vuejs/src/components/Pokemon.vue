<template>
    <div class="Pokemon">
        <router-link :to="`/pokemon/${infoPokemon.id}`" target="_blank">
            <div class="pokemon-card" :class="backgroundColor">

                <h1>Génération : {{ infoPokemon.apiGeneration }}</h1>

                <h2>{{ infoPokemon.name }}</h2>

                <img id="Image_Pokemon" :src="infoPokemon.image">

                <div class="pokemon-type" v-for="type, _ in infoPokemon.apiTypes">
                    <p> <b> Type: {{ type.name }} <img id="Image_type" :src="type.image" :alt="type.type"> </b></p>
                </div>
            </div>
        </router-link>
    </div>
</template>

<script>
export default {
    name: "Pokemon",
    props: ['infoPokemon'],

    data() {
        return {
            pokemon: {}
        }
    },

    computed: {
        backgroundColor() {
            return this.infoPokemon.apiTypes[0].name.toLowerCase();
        }
    },
}
</script>

<style>
* {
    box-sizing: border-box;
    font-family: 'Roboto', sans-serif;
    color: #000;
}

.pokemon-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
}



.pokemon-card {
    width: 340px;
    height: 450px;
    border: 3px solid black;
    border-radius: 10px;
    padding: 20px;
    margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    flex: 0 0 calc(33.33% - 20px);

}

#Image_Pokemon {
    width: 50%;
}

#Image_type {
    width: 6%;
}

.pokemon-type {
    margin: -15px;
    text-align: center;
}

.plante {
    background-color: #3DA225;
}

.eau {
    background-color: #2681F0;
}

.feu {
    background-color: #E72325;
}

.psy {
    background-color: #F03F7A;
}

.électrik {
    background-color: #FAC201;
}

.fée {
    background-color: #F071EF;
}

.acier {
    background-color: #60A3BA;
}

.combat {
    background-color: #FF8100;
}

.dragon {
    background-color: #4F60E2;
}

.glace {
    background-color: #3DD9FF;
}

.insecte {
    background-color: #92A313;
}

.normal {
    background-color: #A1A2A1;
}

.poison {
    background-color: #923FCC;
}

.roche {
    background-color: #B0AB82;
}

.sol {
    background-color: #92501B;
}

.spectre {
    background-color: #713F71;
}

.ténèbre {
    background-color: #4F3E3D;
}

.vol {
    background-color: #82BBF0;
}
</style>