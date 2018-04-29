<template>
  <div>
    {{cep}}
    <input class="teste" type="text" placeholder="Digite o CEP" v-model="cep">
    <p>{{posts.bairro}}</p>
    <p>{{erros}}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'BuscaCep',
  data () {
    return {
      cidade: '',
      cep: '22244400',
      posts: [],
      erros: ''
    }
  },
  methods: {
    getCity: function () {
      axios.get('https://viacep.com.br/ws/' + this.cep + '/json').then(response => {
        this.posts = response.data
        this.posts.erro === true ? this.erros = 'CEP NÃO ENCONTRADO' : console.log('falso')
      })
        .catch(e => {
          console.log('teste erros')
        })
    }
  },
  mounted: function () {
    this.getCity()
  }
}
console.log('Aqui chega 1')
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
