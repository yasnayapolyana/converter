<template>
  <div id="app">
    <Converter />
  </div>
</template>

<script>
import Converter from './components/Converter.vue'

export default {
  name: 'app',
  components: {
    Converter
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,700');

body {
  background-color: #EEEEEE;
  font-family: 'Montserrat', sans-serif;
  display: grid;
  grid-template-rows: auto;
  justify-items: center;
  align-items: center;
}
body, html {
  margin: 0;
  height: 100%;
}
#app {
    width: 28%;
    padding-bottom: 700px;
}
</style>
