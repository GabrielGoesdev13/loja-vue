<template>
  <div class="produtos-page">
    <h1>Produtos</h1>

    <!-- Barra de busca e filtro -->
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

    <!-- Lista de produtos -->
    <div class="produtos-grid">
      <div
        v-for="produto in produtosFiltrados"
        :key="produto.id"
        class="produto-card"
      >
        <div class="produto-imagem">{{ produto.icone }}</div>
        <h3>{{ produto.nome }}</h3>
        <p class="produto-categoria">{{ produto.categoria }}</p>
        <p class="produto-preco">R$ {{ produto.preco.toFixed(2) }}</p>
        <button @click="$emit('adicionar', produto)" class="btn-adicionar">
          Adicionar ao Carrinho
        </button>
      </div>
    </div>

    <!-- Mensagem quando não encontra produto -->
    <p v-if="produtosFiltrados.length === 0" class="sem-produtos">
      Nenhum produto encontrado.
    </p>
  </div>
</template>

<script>
export default {
  name: 'ProdutosView',
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
    // Lista de categorias únicas
    categorias() {
      return [...new Set(this.produtos.map(p => p.categoria))]
    },
    // Filtra produtos por busca e categoria
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

.produto-card {
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  text-align: center;
  transition: 0.3s;
}

.produto-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 16px rgba(0,0,0,0.15);
}

.produto-imagem {
  font-size: 3rem;
  margin-bottom: 12px;
}

.produto-categoria {
  color: #888;
  font-size: 0.85rem;
  margin: 4px 0;
}

.produto-preco {
  font-size: 1.2rem;
  font-weight: bold;
  color: #2c3e50;
  margin: 8px 0 16px;
}

.btn-adicionar {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: 0.3s;
  width: 100%;
}

.btn-adicionar:hover {
  background-color: #2980b9;
}

.sem-produtos {
  text-align: center;
  color: #888;
  font-size: 1.1rem;
  margin-top: 48px;
}
</style>