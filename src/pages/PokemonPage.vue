<template>
  <h1 v-if="!pokemonCorrecto">Porfavor espere............</h1>
  <div v-else>
    <h1>Selecciona el Pokemon Correcto</h1>
    <PokemonImagen :idPokemon="pokemonCorrecto.id" :mostrarPokemon="mostrar"/>
    <PokemonOpciones v-show="!mensaje" :pokemons="arreglo" @seleccionPokemon="revisarRespuesta($event)"/>
    <div v-if="inicio">
      <p v-show="mensaje" > Haz seleccionado el pokemon correcto: {{nombre}}</p>
    </div>

    <div v-if="msjE">
      <p v-show="mensaje" > Haz seleccionado el pokemon incorrecto: {{error}}</p>    
    </div>
    
    

  </div>
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";
import obtenerPokemonsFachada from "../clientes/ClientePokemonAPI.js"

export default {
  data(){
        return{
            arreglo: [],
            pokemonCorrecto: null,
            mostrar : false,   
            mensaje: false,
            inicio: false,
            msjE: false,
            nombre: "",
            error: "",
        };
    },
    components:{
        PokemonImagen,
        PokemonOpciones,
    },
    methods:{
      async cargaInicial(){
        const vectorInicial= await obtenerPokemonsFachada(7);
        this.arreglo = vectorInicial;
        const indice = Math.floor(Math.random()*7);
        this.pokemonCorrecto = this.arreglo[indice];
      },
      revisarRespuesta(dato){
        console.log('se emitio un evento desde el hijo');
        console.log(dato);
        if (dato.ind === this.pokemonCorrecto.id) {
          this.mostrar=true;
          this.mensaje=true;
          this.inicio= true;
          this.nombre = dato.nom;
        }else{
          this.msjE = true;
          this.mensaje=true;
          this.error = "pokemon incorrecto"
          console.log('ERROR')
        }

      },
    },

    mounted(){
      console.log('Entro')
      this.cargaInicial();

    },

};
</script>

<style>

</style>