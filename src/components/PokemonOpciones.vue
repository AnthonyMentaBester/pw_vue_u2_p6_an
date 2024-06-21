<template>
    <div class="opciones-container">
        <ul>
            <li v-for="pokemon in pokemons" :key="pokemon.id">{{pokemon.name}}</li>
        </ul>

    </div>
</template>

<script>
export default {
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

}

li:hover{
    background-color: rgba(0, 0, 0, 0.32);
}
.opciones-container{
    display: flex;
    justify-content: center;
}
</style>