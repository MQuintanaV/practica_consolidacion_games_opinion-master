<template>
  <div class="home">
    <h1>Lista de Juegos Disponibles</h1>
    <audio controls>
          <source src="../assets/retro.mp3" type="audio/mp3">

        </audio>
    <Juegos></Juegos>


  </div>
</template>

<script>
// @ is an alias to /src
import Juegos from '@/components/Juegos.vue';

export default {
  name: 'HomeView',
  components: {
    Juegos
  }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script&family=Orbitron:wght@600&display=swap');
.home{
  background-color: #F4ECF7;  
 }
 h1{
  font-family: 'Dancing Script', cursive;
font-family: 'Orbitron', sans-serif;
 }

</style>
