<template>
    <div>
        <h1>{{numero}} {{name | upper}}</h1>
        <p>{{url}} </p>
    </div>
</template>

<script>
export default {
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
    }
}
</script>

<style>

</style>