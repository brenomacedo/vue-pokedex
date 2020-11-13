<template>
    <div>
        <h1>{{ num }}-{{ name }}</h1>
        <p>{{ url }}</p>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Pokemon',
    props: {
        name: String,
        url: String,
        num: Number
    },
    created: async function () {
        const pokemon = await axios.get(this.url)
        this.pokemon.type = pokemon.data.types[0].type.name
        this.pokemon.front = pokemon.data.sprites.front_default
        this.pokemon.back = pokemon.data.sprites.back_default
    },
    data() {
        return {
            pokemon: {}
        }
    }
}
</script>

<style scoped>
    h1 {
        text-transform: capitalize;
    }
</style>