<template>
    <div id="pok">
        <div class="card">
            <div class="card-image">
                <figure>
                <img :src="correntimg">               
                </figure>
                <button class="button is-medium is-fullwidth" @click="mudarsprite">Alterar posição</button>
            </div>
            <div class="card-content">
                <div class="media">
                <div class="media-left">
                   
                </div>
                <div class="media-content">
                    <p class="title is-4">{{numero}} {{name | upper}}</p>
                    <p class="subtitle is-6">{{pokemom.type}}</p>
                </div>
                </div>

                <div class="content">
                </div>
            </div>
            </div><!--------Fim fo card--------------->

    </div>
</template>

<script>
import axios from 'axios';
export default {
    created: function(){
        //chamandi url
        axios.get(this.url).then(res=>{
            this.pokemom.type= res.data.types[0].type.name;
            this.pokemom.front= res.data.sprites.front_default;
            this.pokemom.back= res.data.sprites.back_default;
            this.correntimg=this.pokemom.front;
            console.log(this.pokemom)
        })
    },
    data(){
        return{
            isfront: true,
            correntimg:"",
            pokemom:
                {type:"",
                    front:"",
                    back:""
                }
        }
    },
    props:{
        numero:Number,
        name:String,
        url:String
    },
    filters:{
        upper: function(value){
            //Separei a primeira letra e coloquei em maiuscula e concatenei
            // ela com o resto das letras apartir da segunda letra em diante
            var newName= value[0].toUpperCase() + value.slice(1)
            return newName
        }
    },
    methods:{
        mudarsprite: function(){
            if(this.isfront){
                this.correntimg=this.pokemom.back
                this.isfront= false
            }else{   
                this.correntimg=this.pokemom.front
                this.isfront=true 
            }
        } 
    }
}
</script>

<style>
    #pok{
        margin: 2%;
    }
</style>