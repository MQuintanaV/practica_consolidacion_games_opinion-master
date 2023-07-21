<template>
    <div id="Juegos">
        <h1>Componente Juegos</h1>

        <div class="contenedorPadre">
                <div v-for="(juego,index) in juegos" v-bind:key="index" class="card m-2 cardGeneral orderPoster" style="width: 18rem;">
                        <img v-bind:src="juego.background_image" class="card-img-top" alt="logo">
                        <div class="card-body">
                            <h5 class="card-title">{{juego.name}}</h5>
                            <p class="card-text">ESRB Rating: {{  juego.esrb_rating.name }}</p>
                        </div>
                        <ul class="list-group list-group-flush colorList">
                            <li class="list-group-item">Rating: {{ juego.rating }}</li>
                            <li class="list-group-item">Released: {{  juego.released }}</li>
                            <li class="list-group-item">Updated: {{  juego.updated }}</li>
                        </ul>
                        <div class="card-body">
                            <a v-on:click="mostrarOpiniones(juego.name)" class="btn btnOpinar">Opinar</a>
                            <a v-on:click="irAdministracion(juego.name)" class="btn btnLike">Like</a>
                        </div>
                </div>
        </div>

    </div>
</template>

<script>
import axios from 'axios';
export default{
    name:'Juegos',
    data:function(){
        return{
            cantidadJuegos:0,
            juegos:[],
        }
    },
    methods:{
        consumirApi:function(){

            // let url='https://api.rawg.io/api/games?key=77c79575495e4380b43ff38d0f1cb43f';
            let url='https://api.rawg.io/api/games?key=548ac8fcc5ad4b3780b81ed0b0a992c6';
            axios(url)
            .then(respuesta =>{
                // console.log(respuesta);
                this.cantidadJuegos = respuesta.data.results.length;
                // lógica para acumular en el arreglo juegos cada juego de las distintas paginas
                for(let i=0; i < this.cantidadJuegos; i++){
                    // console.log(respuesta.data.results[i]);
                    this.juegos.push(respuesta.data.results[i]);
                }
            })
            .catch(error=>{
                console.log(error);
            });
        },
        mostrarOpiniones:function(nombreJuego){
            this.$router.push(`/opiniones/${nombreJuego}`);
        },
        irAdministracion:function(nombreJuego){
            this.$router.push(`/administracion/${nombreJuego}`);
        },
    },
    created(){
        this.consumirApi();
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script&family=Orbitron:wght@600&display=swap');
h1{
  font-family: 'Dancing Script', cursive;
font-family: 'Orbitron', sans-serif;
 }
#Juegos{
    background-color: #F4ECF7;
}
.contenedorPadre{
    display:flex;
    flex-wrap: wrap;
    justify-content: center;
}
.cardGeneral{
    background-color: #D2B4DE ;
}
.colorList{
    background-color: #8E44AD;
}
.btnOpinar{
    background-color: #7D3C98;
    color:#F4ECF7;
    transition: 1.2s;
}
.btnOpinar:hover{
    transform: scale(1.2);
}
.btnLike{
    background-color: #3498DB;
    transition: 1.2s;
}
.btnLike:hover{
    transform: scale(1.2);
}
.orderPoster {
    transition: .2s;
    box-shadow: 8px 8px red;
    background-color: white;
    

}

.orderPoster:hover {
    transform: scale(1.2);
    z-index: 1;
}
</style>