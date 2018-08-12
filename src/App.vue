<template>
  <div id="app"  class="">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: "App",
  data(){
  
  },

};
</script>

<style>
#app {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  height: 100%;
  background: url(pages/img/HallstattAustria_PT-BR9407016733_1920x1080.jpg);
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
    background-repeat: no-repeat;
  background-position: center;
  background-size: cover;

}
    .bg-blur {
  float: left;
  width: 100%;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  -webkit-filter: blur(2px);
  -moz-filter: blur(2px);
  -o-filter: blur(2px);
  -ms-filter: blur(2px);
  filter: blur(2px);
}
</style>
