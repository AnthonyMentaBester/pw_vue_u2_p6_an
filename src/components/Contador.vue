<template>
    <h2>{{presentar}}</h2>

    <p>{{numero}} <sup>2</sup> = {{calcular}}</p>




    <div>
        <button v-on:click = "incrementar">+1</button>
        <button @click="disminuir" >-1</button>
    </div>
    
  
</template>

<script>
export default {
   //primera forma de declara un props (basica)
   // props:["titulo", "num"],
   props:{
    titulo: String,
    num: {
        type: Number,
        required: false, 
        default: 10,
        validator(value){
            return value>0;

        }
    }

   },
    data(){
        return{
            numero: this.num,
        };
    },
    methods:{
        calcularCuadrado(){
            console.log('ingreso al metodo');
            return this.numero * this.numero;
        },
        incrementar(){
            this.numero++;
        },
        disminuir(){
            this.numero--;
        }
    },
    computed:{
        calcular(){
            console.log('ingreso a la propiedad computada');
            return this.numero * this.numero;
        },
        presentar(){
            if(this.titulo !== undefined){
                return this.titulo;
            }else{
                return "texto que quiero"
            }
        }
    },


};
</script>

<style>

button{
    background: #64B687;
    border-radius: 5px;
    border: 1px solid white;
    color: white;
    margin: 0px 5px;
    padding: 20px 20px;
    cursor: pointer;
}

button:hover{
     background: #3f644f;

}
</style>
