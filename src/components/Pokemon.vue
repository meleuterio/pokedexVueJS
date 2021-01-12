<template>
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="imgAtual" alt="1° Geração Pokemons">
                </figure>
            </div>

            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{ num }} - {{ name | upper }}</p>
                        <p class="subtitle is-6">{{ pokemon.type }}</p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-success is-outlined" @click="rodarPokemon">Rodar Pokemon</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            pokemon: {
                type: '',
                front: '',
                back: ''
            },
            isFront: true,
            imgAtual: ''
        }
    },
    async created() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.imgAtual = this.pokemon.front
        })
    },
    props: {
        name: String,
        url: String,
        num: Number
    },
    methods: {
        rodarPokemon() {
            if(this.isFront) {
                this.isFront = false
                this.imgAtual = this.pokemon.back
            } else {
                this.isFront = true
                this.imgAtual = this.pokemon.front
            }
        }
    },
    filters: {
        upper(value) {
            var newName = value[0].toUpperCase() + value.slice(1)
            return newName
        }
    }
}
</script>

<style scoped>
    #pokemon {
        margin-top: 2%;
    }
</style>