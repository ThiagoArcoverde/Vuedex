<template>
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="currentImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{ dexNumber }} - {{ toCapitalize(name) }}</p>
                        <p class="subtitle is-6"> {{ pokemon.type }} </p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-medium is-fullwidth" @click="changeSprite">Mudar sprite</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    created: function () {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.frontSprite = res.data.sprites.front_default
            this.pokemon.backSprite = res.data.sprites.back_default
            this.currentImg = this.pokemon.frontSprite
        })
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                frontSprite: '',
                backSprite: ''
            }
        }
    },
    props: {
        dexNumber: Number,
        name: String,
        url: String
    },
    methods: {
        toCapitalize: function (value) {
            return value[0].toUpperCase() + value.slice(1)
        },
        changeSprite: function(){
            if(this.isFront){
                this.currentImg = this.pokemon.backSprite
            }else{
                this.currentImg = this.pokemon.frontSprite
            }
            this.isFront = !this.isFront
        }
    }
}
</script>

<style>
#pokemon {
    margin-top: 2%;
    margin-bottom: 2%;
}
</style>
