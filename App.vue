<template>
  <div id="App">
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator'
export default {
  // name: 'App',
  components: {
    Calculator
  }
}
</script>

<style lang="css">
  body {
    background-color: #222;
    margin: 0;
    padding: 0;
  }
  
  #app {
    font-family: 'Avenir', Helvetica, Arial;
    text-align: center;
    color: #fff;
  }
</style>