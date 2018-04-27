<template>
  <div>
    <input class="teste" type="text" placeholder="Digite o CEP" v-model="cep">
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'BuscaCep',
  data () {
    return {
      cep: '20081130'
    }
  },
  created () {
    axios.get('https://viacep.com.br/ws/' + this.cep + '/json').then(response => {
      this.posts = response.data
    })
      .catch(e => {
        this.errors.push(e)
      })
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
