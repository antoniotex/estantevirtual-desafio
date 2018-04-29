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
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
