<template>
    <div class="opciones-container">
        <ul>
            <li v-for="pokemon in pokemons" :key="pokemon.id" @click="$emit('seleccionPokemon', {ind:pokemon.id,nom:pokemon.nombre, test1:'esto es una prueba', test2:test3})">{{pokemon.nombre}}</li>
        </ul>

    </div>
</template>

<script>
export default {
    data(){
        return{
            test3: 'prueba',
        };
    },
    props:{
        pokemons:{
            type: Array,
            required: true,
            
        },
    },

}
</script>

<style>
ul{
    list-style-type: none;
}
li{
    border: 1px solid rgba(0, 0, 0, 1);
    border-radius: 5px;
    margin-bottom: 10px;
    width: 250px;
    background-color: white;
    cursor: pointer;
    padding: 20px;

}

li:hover{
    background-color: rgba(0, 0, 0, 0.32);
}
.opciones-container{
    display: flex;
    justify-content: center;
}
</style>