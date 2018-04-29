<template>
  <div>
    <input class="teste" type="text" placeholder="Digite o CEP" v-model="cep" maxlength="8">
    <p>{{rua}}</p>
    <p>{{cidade + uf}}</p>
    <p>{{erros}}</p>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'BuscaCep',
  data () {
    return {
      rua: '',
      cidade: '',
      uf: '',
      cep: '',
      posts: [],
      erros: ''
    }
  },
  methods: {
    getCity: function () {
      axios.get('https://viacep.com.br/ws/' + this.cep + '/json').then(response => {
        this.posts = response.data
        if (this.posts.erro === true) {
          this.erros = 'CEP NÃO ENCONTRADO'
        } else {
          this.rua = response.data.logradouro
          this.cidade = response.data.localidade + ', '
          this.uf = response.data.uf
        }
      })
        .catch(e => {
          this.erros.push(e)
        })
    }
  },
  watch: {
    cep: function () {
      if (this.cep.length === 8) {
        this.getCity()
        this.erros = ''
      }
      if (this.cep.length < 8 && this.cep.length > 0) {
        this.erros = 'Cep invalido'
        this.rua = ''
        this.cidade = ''
        this.uf = ''
      } else {
        this.erros = ''
      }
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
