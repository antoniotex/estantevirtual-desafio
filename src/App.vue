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
*{
  padding: 0;
  margin: 0;
  list-style: none;
}
html, body{
  height: 100%;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: 3px solid red;
  height: 100%;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
