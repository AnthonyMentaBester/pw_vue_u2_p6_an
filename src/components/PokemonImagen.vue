<template>
    <div class="pokemon-container">
        <img  v-show="mostrarPokemon" :src="imagenSRC" alt="No se pudo visualizar la imagen">

        <img v-show="!mostrarPokemon" class="oculta-pokemon" :src="imagenSRC" alt="No se pudo visualizar la imagen">
    </div>  

</template>

<script>
export default {
     data(){
        return{
            mostrar: true,
        };
    },
    props:{
        idPokemon:{
            type: Number,
            required: true,

        },
        mostrarPokemon:{
            type: Boolean,
            required: true,
        },

    },
    computed:{
        imagenSRC(){
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.idPokemon}.svg`;
        },

    },

};

</script>

<style scoped>
.oculta-pokemon{
    filter: brightness(0);
}
img{
    height: 400px;
    width: 200px;
    position: absolute;
    right: 45%;
}

.pokemon-container {
    
    height: 400px;
}
</style>