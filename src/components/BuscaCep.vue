<template>
  <div>
    <input type="text" placeholder="Digite o CEP" v-model="cep">
  </div>
</template>

<script>
export default {
  name: 'BuscaCep',
  data () {
    return {
      cep: ''
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
