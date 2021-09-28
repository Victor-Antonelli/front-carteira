<template>
  <div class="cartao">
    <div class="titulo-cartao">
      <h1>Banco Padrão</h1>
      <button v-if="id > 0" class="delete" type="button" @click="remove(id)">Excluir Cartao</button>
    </div>
    <div class="dados-cartao">
      <span class="numero-cartao">{{ numeroCartao }}</span>
      <span class="nome-cartao">{{ nome }}</span>
      <span class="data-validade">{{ validade }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'

export default Vue.extend({
  props: {
    id: Number,
    numeroCartao: String,
    nome: String,
    validade: String,
  },
  methods: {
    remove(id: Number){
      axios.delete(`http://localhost:3030/cartao/${id}`)
      .then(function(response){
        console.log(response)
      })
      .catch(function(error){
        console.warn(error)
      })      
    },  
  }
})
</script>

<style scoped>

.cartao{
  width: 450px;
  height: 250px;
  background-color: rgba(0, 0, 0, 0.1);
  border-radius: 20px;
  padding: 15px;
  box-sizing: border-box;
  margin-bottom: 10px;
  transition: ease 0.2s;

}

.cartao:hover {
  transform: scale(1.05,1.05);
  transition: ease 0.2s;
}

.titulo-cartao{
  color: #000;
  display: block;
}

.titulo-cartao h1 {
  font-size: 1.3rem;
}

.dados-cartao{
  margin-top: 80px;
}
.numero-cartao{
  display: block;
  font-weight: 600;
  font-size: 1.4rem;
}


.nome-cartao, .data-validade{
  display: block;
  margin-top: 5px;
  font-size: 1.2rem;
}

.delete{
  margin: 10px 0;
  padding: 10px;
  border-radius: 10px;
  background-color: #db3030;
  color: #FFF;
  border: none;

}
</style>