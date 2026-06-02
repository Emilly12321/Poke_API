<template>

    <div class="m-5">
        <div class="card has-background-grey-lighter ">
            <div class="card-image is-flex is-justify-content-center ">
                <figure>
                    <img :src="currentIMG" alt="Placeholder image" />
                </figure>
            </div>
            <div class="card-content ">
                <div class="media">
                    <div class="media-content x">
                        <p class="title is-5 has-text-dark"> {{ num }} - {{ upper(name) }} </p>
                        <p class="subtitle is-6 has-text-dark">{{ pokemon.type }}</p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-medium is-fullwidth has-background-danger" @click="mudarImagem">Virar o pokemon</button>
                </div>
            </div>
        </div>


    </div>

</template>

<script>
import axios from 'axios';

export default {
    created: function () {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default
            this.currentIMG = this.pokemon.front;
            console.log(this.pokemon)
        })
    },
    data() {
        return {

            isFront: true,
            currentIMG: '',
            pokemon: {
                type: '',
                front: '',
                back: '',
            }

        }

    },
    props: {
        num: Number,
        name: String,
        url: String

    },
    methods: {
        upper: function (pokemon) {
            // Podemos tratar uma string como uma array, pegamos abaixo a primeira letra do nome do pokemon, logo após colocamos ela em maiúscula com a function e logo em seguida retiramos a duplicidade de letras iniciais em maiúsculo.
            let nome = pokemon[0].toUpperCase() + pokemon.slice(1);
            return nome;
        },
        mudarImagem: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentIMG = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentIMG = this.pokemon.front;

            }
        }
    }
}


</script>