<template>
  <div>
    {{cep}}
    <input class="teste" type="text" placeholder="Digite o CEP" v-model="cep" maxlength="8">
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
      cep: '',
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
  watch: {
    cep: function () {
      if (this.cep.length === 8) {
        console.log('Chegou em 8!!!')
        this.getCity()
        this.erros = ''
      }
      if (this.cep.length < 8) {
        console.log('menor que 8')
      }
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
