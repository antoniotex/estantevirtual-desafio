<template>
  <div class="container">
    <h1>Cadastro de Endereços</h1>
    <div class="cadastro">
      <input type="text" placeholder="Digite o nome..." v-model='nome'><br/>
      <input id="cep-campo" type="text" placeholder="Digite o CEP" v-model="cep" maxlength="8"><br/>
      {{erros}}
      {{rua}}<br/>
      <button class="add-cep" v-on:click='addCep'>Add Cep</button>
    </div>
    <div class="card-container">
      <ul>
        <li class="card" v-for='(item, key) in arma' :key='item.id'>
          <h3>Nome: {{item.nome}}</h3>
          <h4>{{item.rua + ', ' + numero}}</h4>
          <h4>{{item.cidade + ', ' + item.uf}}</h4>
          <button class="edit-button">Editar</button>
          <button class="del-button" v-on:click='delCep(key)'>Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'BuscaCep',
  data () {
    return {
      nome: '',
      rua: '',
      numero: '20',
      cidade: '',
      uf: '',
      cep: '',
      erros: '',
      arma: []
    }
  },
  methods: {
    addCep: function (e) {
      this.arma.push({nome: this.nome, rua: this.rua, cidade: this.cidade, uf: this.uf})
      this.cep = ''
      alert('Endereço armazenado!!')
    },
    delCep: function (index) {
      this.arma.splice(index, 1)
    },
    getCity: function () {
      axios.get('https://viacep.com.br/ws/' + this.cep + '/json').then(response => {
        this.posts = response.data
        if (response.data.erro === true) {
          this.erros = 'CEP NÃO ENCONTRADO'
          document.getElementById('cep-campo').style.background = 'rgba(255, 0, 0, 0.4)'
        } else {
          this.rua = response.data.logradouro
          this.cidade = response.data.localidade
          this.uf = response.data.uf
          document.getElementById('cep-campo').style.background = 'rgba(0, 255, 0, 0.3)'
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
        document.getElementById('cep-campo').style.background = 'none'
      }
      if (this.cep.length < 8 && this.cep.length > 0) {
        // document.getElementById('cep-campo').style.background = 'red'
        this.erros = 'Cep invalido'
        this.rua = ''
        this.cidade = ''
        this.uf = ''
      } else {
        this.erros = ''
        document.getElementById('cep-campo').style.background = 'none'
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
<style scoped>
  .container{
    width: 100%;
    border: 2px solid green;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .cadastro{
    width: 30%;
  }
  input{
    width: 100%;
    border: 1px solid #bbb;
    border-radius: 6px;
    height: 40px;
    outline: none;
  }
  #cep-campo{
    background: none;
  }
  .card-container ul{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }
  .card{
    width: 30%;
    margin: 10px;
    padding: 10px;
    border: 2px solid blue;
  }
  .del-button, .edit-button, .add-cep{
    border-radius: 10px;
    padding: 5px 10px;
    border: none;
    font-weight: bold;
  }
  .del-button{
    background: #f00;
  }
  .add-cep{
    background: #0c0;
    width: 100%;
    height: 40px;
  }
</style>
