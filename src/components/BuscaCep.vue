<template>
  <div>
    <input class="teste" type="text" placeholder="Digite o CEP" v-model="cep" maxlength="8">
    <button v-on:click='addCep'>Add Cep</button>
    <p>{{rua}}</p>
    <p>{{cidade + uf}}</p>
    <p>{{erros}}</p>
    <ul>
      <li v-for='(item, key) in arma' :key='item.id'>
        {{item}}
        <button v-on:click='delCep(key)'>Exclui Cep</button>
      </li>
    </ul>
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
      erros: '',
      arma: []
    }
  },
  methods: {
    addCep: function (e) {
      this.arma.push({rua: this.rua, cidade: this.cidade, uf: this.uf})
      this.cep = ''
    },
    delCep: function (index) {
      this.arma.splice(index, 1)
    },
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
          console.log(e)
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
    },
    arma: {
      handler () {
        console.log('Todos changed!')
        localStorage.setItem('arma', JSON.stringify(this.arma))
      },
      deep: true
    }
  },
  mounted () {
    console.log('App mounted!')
    if (localStorage.getItem('arma')) this.arma = JSON.parse(localStorage.getItem('arma'))
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
