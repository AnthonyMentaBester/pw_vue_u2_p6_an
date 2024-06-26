<template>
    <div class="puntaje-container">
        <p type="Puntaje: ">{{ puntajeJuego }}</p>
        <p type="Intentos: ">{{ tiradasJuego }}</p>
    </div>
</template>

<script>
export default{
    data() {
        return {
            puntajeJuego: 0,
        }
    },
    props:{
        tiradasJuego:{
            type: Number,
            required:true,
            default:0,
        },
        intentosJuego:{
            type: Boolean,
            required:true,
            default:0,
        },

    },
    watch: {
        intentosJuego(newVal) {

            switch (this.tiradasJuego) {
                case 0:
                    this.puntajeJuego = 0;
                    break;
                case 1:
                    this.puntajeJuego = 10;
                    break;
                case 2:
                    this.puntajeJuego = 8;
                    break;
                case 3:
                    this.puntajeJuego = 5;
                    break;
                case 4:
                    this.puntajeJuego = 3;
                    break;
                case 5:
                    this.puntajeJuego = 2;
                    break;
                case 6:
                    this.puntajeJuego = 1;
                    break;
                case 7:
                    this.puntajeJuego = 0;
                    break;

                default:
                    this.puntajeJuego = 0;
                    break;
            }

        }
    }
}

</script>

<style scoped>

.puntaje-container{
    
    display: grid;
    grid-template-columns: 700px 700px;
    grid-template-rows: 100px;
    justify-content: center;
    align-items: center;
}
p:before{
    content: attr(type);
    font-size: 5vh;
    color: black;
}

p{
    font-size: 5vh;
    color: black;
}


</style>