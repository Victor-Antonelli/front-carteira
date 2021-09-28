<template>
  <div class="container_create_cartao">
    <div class="form_container">
      <form action="">
        <label> Numero do Cartao
          <input type="text" class="iptTxt" name="numero" id="numero" v-model="numero" >
        </label>
        <label> Nome no Cartao
          <input type="text" class="iptTxt" name="nome" id="nome" v-model="nome">
        </label>
        <label> Data de Validade
          <input type="text" class="iptTxt" name="validade" id="validade" v-model="validade">
        </label>
        <label> CVV
          <input type="text" class="iptTxt" name="cod_seguranca" id="cod_seguranca" v-model="cod_seguranca">
        </label>
        <button class="btnSend" form="#" @click="salvar">Salvar</button>
      </form>
    </div>
    <div class="card_container">
      <Cartao :numeroCartao="numero"
      :nome="nome" :validade="validade"  /> 
    </div>
  </div>  
</template>

<script lang='ts'>
import Vue from 'vue'
import axios from 'axios'

export default Vue.extend({
  data() {
    return {
      numero: ''
    , nome: ''
    , validade: ''
    , cod_seguranca: ''
    }
  },
  methods: {
    limpar(){
      this.numero = ''
      this.nome = ''
      this.validade = ''
      this.cod_seguranca = ''
    },
    salvar(){
      axios.post('http://localhost:3030/cartao', {
        numero: this.numero,
        nome: this.nome,
        validade: this.validade,
        cod_seguranca: this.cod_seguranca
      })
      .then(response => {
        alert('Cartao cadastrado com sucesso!')
        this.limpar()
      })
      .catch(function(error){
        console.warn(error)
      })

    }
  }  
})
</script>

<style  scoped>
  .container_create_cartao{
    display: flex;
    justify-content: center;
    align-items: space-between;
  }
  .form_container{
    display: flex;
    flex-wrap: wrap;
    width: 50%;
    justify-content: center;
  }
  .form_container label {
    display: block;
    margin: 10px 0;
    text-align: right;
  }

  .iptTxt{
    border: 1px solid #002a6e;
    border-radius: 10px;
    height: 30px;
  }
  
  .btnSend{
    color: #FFF;
    background-color: #00FF00;
    padding: 10px;
    box-sizing: border-box;
    border: none;
    border-radius: 10px;
  }
</style>
