<template>
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="isFront ? pokemon.front : pokemon.back" @click="changePic"
                    alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                <div class="media-content">
                    <p class="title is-4 pokename">{{ num }} - {{ name }}</p>
                    <p class="subtitle is-6">{{ pokemon.type }}</p>
                </div>
                </div>

                <div class="content">
                
                </div>
            </div>
        </div>
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
            pokemon: {
                type: '',
                front: '',
                back: ''
            },
            isFront: true
        }
    },
    methods: {
        changePic: function () {
            this.isFront = !this.isFront
        }
    }
}
</script>

<style scoped>
    .pokename {
        text-transform: capitalize;
    }

    #pokemon {
        margin-top: 6px;
    }

    img {
        cursor: pointer;
    }
</style>