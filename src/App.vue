<template>
<div class="parent">
  <div class="main">
  <HeaderMeteo />

  <InfoMeteo />

  <autrejours />
  </div>


</div>
</template>

<script>
import HeaderMeteo from './components/HeaderMeteo.vue'
import InfoMeteo from './components/ImageMeteo.vue'
import autrejours from './components/autreJours.vue'

export default {
  name: 'App',
  components: {
    HeaderMeteo,
    InfoMeteo,
    autrejours
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

*{
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.main{
  width: 40%;
}
.parent{
  width: 100%;
  display: flex;
  justify-content: center;
}
@media(max-width:767px){
  .main{
    width: 100%;
  }
}
</style>

