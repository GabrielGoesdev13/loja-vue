<template>
  <div class="carrinho-item">
    <span class="item-icone">{{ item.icone }}</span>
    <div class="item-info">
      <h3>{{ item.nome }}</h3>
      <p>R$ {{ item.preco.toFixed(2) }} x {{ item.quantidade }}</p>
    </div>
    <p class="item-subtotal">R$ {{ (item.preco * item.quantidade).toFixed(2) }}</p>
    <button @click="$emit('remover', item.id)" class="btn-remover">✕</button>
  </div>
</template>

<script>
export default {
  name: 'CartItem',
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  emits: ['remover']
}
</script>

<style scoped>
.carrinho-item {
  display: flex;
  align-items: center;
  gap: 16px;
  background: white;
  border-radius: 12px;
  padding: 16px;
  margin-bottom: 16px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.item-icone {
  font-size: 2rem;
}

.item-info {
  flex: 1;
}

.item-info h3 {
  margin-bottom: 4px;
}

.item-info p {
  color: #888;
  font-size: 0.9rem;
}

.item-subtotal {
  font-weight: bold;
  font-size: 1rem;
}

.btn-remover {
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  cursor: pointer;
  font-size: 1rem;
}
</style>