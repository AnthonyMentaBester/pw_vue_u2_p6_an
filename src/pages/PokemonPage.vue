<template>
  <h1 v-if="!pokemonCorrecto">Porfavor espere............</h1>
  
  
  <div v-else>
    <h1>Selecciona el Pokemon Correcto</h1>
    <PokemonPuntaje :tiradasJuego="totalIntentos" :intentosJuego="mensaje" />
    <PokemonImagen :idPokemon="pokemonCorrecto.id" :mostrarPokemon="mostrar"/>
    <p v-show="mensaje" > Haz seleccionado el pokemon correcto: {{nombre}}</p>
    
    <div v-if="inicio">

      <p v-show="!mensaje" > Haz seleccionado el pokemon incorrecto: {{error}}</p> 
      
    </div>
    <div v-show="!mensaje">
      <PokemonOpciones :pokemons="arreglo" @seleccionPokemon="revisarRespuesta($event)"/> 

    </div>
    
    <div v-show="mensaje">
      <button @click="reiniciar()">Reiniciar</button>
    </div>  
  </div>

</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";
import obtenerPokemonsFachada from "../clientes/ClientePokemonAPI.js"
import PokemonPuntaje from "../components/PokemonPuntaje.vue"

export default {
  data(){
        return{
            arreglo: [],
            pokemonCorrecto: null,
            mostrar : false,   
            mensaje: false,
            inicio: false,
            nombre: "",
            error: "",
            totalIntentos: 0,
        };
    },
    components:{
        PokemonImagen,
        PokemonOpciones,
        PokemonPuntaje,
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
        this.totalIntentos++;

        if (dato.ind === this.pokemonCorrecto.id) {
          this.mostrar=true;
          this.mensaje=true;
          this.nombre = dato.nom;
          
        }else{
          this.inicio = true;
          this.error = "pokemon incorrecto"
          console.log('ERROR')
        }

      },
      reiniciar() {
        this.totalIntentos = 0;
        this.mensaje = false;
        
        this.inicio = false;
        
        this.mostrar = false;  
        this.cargaInicial();    
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