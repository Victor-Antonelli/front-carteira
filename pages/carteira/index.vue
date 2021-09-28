<template>
  <div class="main_container">
    <div class="card_container">
      <Cartao v-for="(cartao, indice) in cartoes" :key="indice" :id="cartao.id" :numeroCartao="cartao.numero"
      :nome="cartao.nome" :validade="cartao.validade"  /> 
    </div>
    <div class="options_container">
      <nav>
        <ul class="menu">
          <li><NuxtLink class="menu-item green" to="cartao/create">Adicionar Cartão </NuxtLink></li>
          <!--li class="menu-item red">Remover</!--li-->
        </ul>
      </nav>
    </div>
  </div>
  
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  layout: 'carteira',
  data() {
    return {
      cartoes : [] 
    }
  },
  async created() {
    this.cartoes = await this.getCartoes()
  },
  methods: {
     getCartoes: async () => {
       return await fetch('http://localhost:3030/carteira').then(res => res.json())
     }
  },
  
})
</script>

<style scoped>
.main_container{
  width: 100%;
  display: flex;
}
.card_container{
  width: 50%;  
  display: flex;
  flex-wrap: wrap;
}

.options_container{
  width: 50%;
  display: flex;
}
nav{
  width: 100%;
  padding: 30px;
  box-sizing: border-box;
}
.menu{
  display: flex;
  align-items: center;
  justify-content: center;
  list-style-type: none;
}

.menu-item {
  margin: 0 10px;
  padding: 15px;
  border-radius: 10px;
}

.menu-item:hover, .menu-item a:hover {
  cursor: pointer;
  color: #FFF;
}

.green{
  background-color: #00ff00;

}

.red{
  background-color: #db3030;
}

a {
  text-decoration: none;
  color: #000;
}
</style>