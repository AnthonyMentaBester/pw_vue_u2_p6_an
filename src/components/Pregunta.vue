<template>
  <img v-if="img!==null" 
  v-bind:src="img" 
  alt="no se cargo">
  <div class="oscuro"></div>
    <div class="pregunta-container">

  
        <input v-model="pregunta" type="text" placeholder="Hazme una Pregunta">
        <p>Recuerda Terminar la pregunta con el signo de interrogacion (?)</p>

        <div v-show="mensaje" class="respuesta">
            <h2>{{pregunta }}</h2>
            <h1>{{respuesta ==='yes'? 'SI!':'NO!'}}</h1>
        </div>
    </div>
  

</template>

<script>
export default {
    data(){
        return{
            pregunta: null,
            respuesta: null,
            img: null,
            mensaje: false,

        };
    },
    watch:{
        pregunta(value, oldValue){
            this.mensaje= false;
            
            if(!value.includes("?")){
                console.log({value, oldValue});
                return; //salgase del observador
            }
            //Consumir el API para obtener la respuesta
            //a esto se refiere con no pober el async
            this.obtenerRespuesta();
            this.mensaje = true;
        },
    },
    methods:{
        async obtenerRespuesta(){
            this.respuesta = "Pensando.................."
            const data = await fetch("https://yesno.wtf/api").then(resp => resp.json())
            console.log(data);
            const {answer,forced,image}=data;
            console.log(answer);
            this.respuesta = answer;
            this.img = image;
            return data;

        }
    },
};

</script>

<style scoped>
img, .oscuro {
    max-width: 100%;
    height: 100vh;
    max-height: 100%;
    width: 100vw;
    position: fixed;
    top: 0px;
    left: 0px;  
}

.oscuro {
    background-color: rgba(0, 0, 0, 0.37);
}
.pregunta-container {
    position: relative;



}

input {
    margin-top: 50px;
    width: 260px;
    padding: 10px 135px;
    border: none;
    border-radius: 5px;
    
}
input:focus{
    outline: none;
}

p, h1, h2 {
    color: white;
}

p {
    font-size: 25px;
    margin-top: 0px;
}

.respuesta{
    margin-top: 290px;
}
body{
    background-color: black;
}



</style>