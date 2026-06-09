<template>
  <div class="produtos-page">
    <h1>Produtos</h1>

    <div class="filtros">
      <input
        v-model="busca"
        type="text"
        placeholder="Buscar produto..."
        class="input-busca"
      />
      <select v-model="categoriaSelecionada" class="select-filtro">
        <option value="">Todas as categorias</option>
        <option v-for="cat in categorias" :key="cat" :value="cat">{{ cat }}</option>
      </select>
    </div>

    <div class="produtos-grid">
      <ProductCard
        v-for="produto in produtosFiltrados"
        :key="produto.id"
        :produto="produto"
        @adicionar="$emit('adicionar', $event)"
      />
    </div>

    <p v-if="produtosFiltrados.length === 0" class="sem-produtos">
      Nenhum produto encontrado.
    </p>
  </div>
</template>

<script>
import ProductCard from '../components/Produtos/ProductCard.vue'

export default {
  name: 'ProdutosView',
  components: {
    ProductCard
  },
  emits: ['adicionar'],
  data() {
    return {
      busca: '',
      categoriaSelecionada: '',
      produtos: [
        { id: 1, nome: 'Notebook', categoria: 'Eletrônicos', preco: 3499.99, icone: '💻' },
        { id: 2, nome: 'Smartphone', categoria: 'Eletrônicos', preco: 1999.99, icone: '📱' },
        { id: 3, nome: 'Camiseta', categoria: 'Roupas', preco: 59.99, icone: '👕' },
        { id: 4, nome: 'Calça Jeans', categoria: 'Roupas', preco: 129.99, icone: '👖' },
        { id: 5, nome: 'Tênis', categoria: 'Calçados', preco: 299.99, icone: '👟' },
        { id: 6, nome: 'Relógio', categoria: 'Acessórios', preco: 199.99, icone: '⌚' },
        { id: 7, nome: 'Fone de Ouvido', categoria: 'Eletrônicos', preco: 149.99, icone: '🎧' },
        { id: 8, nome: 'Mochila', categoria: 'Acessórios', preco: 89.99, icone: '🎒' }
      ]
    }
  },
  computed: {
    categorias() {
      return [...new Set(this.produtos.map(p => p.categoria))]
    },
    
    produtosFiltrados() {
      return this.produtos.filter(p => {
        const nomeBate = p.nome.toLowerCase().includes(this.busca.toLowerCase())
        const categoriaBate = this.categoriaSelecionada === '' || p.categoria === this.categoriaSelecionada
        return nomeBate && categoriaBate
      })
    }
  }
}
</script>

<style scoped>
.produtos-page {
  padding: 32px;
  max-width: 1200px;
  margin: 0 auto;
}

.produtos-page h1 {
  font-size: 2rem;
  margin-bottom: 24px;
}

.filtros {
  display: flex;
  gap: 16px;
  margin-bottom: 32px;
  flex-wrap: wrap;
}

.input-busca, .select-filtro {
  padding: 10px 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
  flex: 1;
  min-width: 200px;
}

.produtos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 24px;
}

.sem-produtos {
  text-align: center;
  color: #888;
  font-size: 1.1rem;
  margin-top: 48px;
}
</style>