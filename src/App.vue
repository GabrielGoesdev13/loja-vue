<template>
  
  <NavBar :totalItens="totalItens" />
  <RouterView :carrinho="carrinho" @adicionar="adicionarItem" @remover="removerItem" />
</template>

<script>
import NavBar from './components/layout/NavBar.vue'

export default {
  name: 'App',
  components: {
    NavBar
  },
  data() {
    return {
     
      carrinho: []
    }
  },
  computed: {
    
    totalItens() {
      return this.carrinho.reduce((total, item) => total + item.quantidade, 0)
    }
  },
  methods: {
    adicionarItem(produto) {
      
      const existente = this.carrinho.find(item => item.id === produto.id)
      if (existente) {
        existente.quantidade++
      } else {
        this.carrinho.push({ ...produto, quantidade: 1 })
      }
    },
    removerItem(produtoId) {
      
      this.carrinho = this.carrinho.filter(item => item.id !== produtoId)
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', sans-serif;
  background-color: #f4f6f8;
  color: #2c3e50;
}

a {
  text-decoration: none;
}
</style>