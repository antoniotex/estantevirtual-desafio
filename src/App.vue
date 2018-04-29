<template>
  <div id="app">
    <BuscaCep/>
  </div>
</template>

<script>
import BuscaCep from './components/BuscaCep'

export default {
  name: 'App',
  components: {
    BuscaCep
  }
}
</script>

<style>
#app {
  border: 3px solid red;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
