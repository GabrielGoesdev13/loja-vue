<template>
  <div class="produto-card">
    <div class="produto-imagem">{{ produto.icone }}</div>
    <h3>{{ produto.nome }}</h3>
    <p class="produto-categoria">{{ produto.categoria }}</p>
    <p class="produto-preco">R$ {{ produto.preco.toFixed(2) }}</p>
    <button @click="$emit('adicionar', produto)" class="btn-adicionar">
      Adicionar ao Carrinho
    </button>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
   
    produto: {
      type: Object,
      required: true
    }
  },
  emits: ['adicionar']
}
</script>

<style scoped>
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
</style>