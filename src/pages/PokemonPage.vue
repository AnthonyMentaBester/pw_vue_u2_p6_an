<template>
<h1>Selecciona el Pokemon Correcto</h1>
  <PokemonImagen :idPokemon="448" :mostrarPokemon="true"/>
  <PokemonOpciones :pokemons="arreglo"/>
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";
import obtenerPokemonsFachada from "../clientes/ClientePokemonAPI.js"

export default {
    components:{
        PokemonImagen,
        PokemonOpciones,
    },
    methods:{
      async cargaInicial(){
        const vectorInicial= await obtenerPokemonsFachada(4);
        this.arreglo = vectorInicial;
      },
    },
    data(){
        return{
            arreglo: [],
        };
    },
    mounted(){
      this.cargaInicial();

    },

};
</script>

<style>

</style>