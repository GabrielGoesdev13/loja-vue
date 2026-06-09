<template>
  <div class="carrinho-page">
    <h1>🛒 Meu Carrinho</h1>

    <div v-if="carrinho.length > 0">
      <CartItem
        v-for="item in carrinho"
        :key="item.id"
        :item="item"
        @remover="$emit('remover', $event)"
      />

      <div class="carrinho-total">
        <h2>Total: R$ {{ total.toFixed(2) }}</h2>
      </div>

      <div class="formulario">
        <h2>Finalizar Compra</h2>

        <input v-model="form.nome" type="text" placeholder="Seu nome completo" />
        <p v-if="erros.nome" class="erro">{{ erros.nome }}</p>

        <input v-model="form.email" type="email" placeholder="Seu e-mail" />
        <p v-if="erros.email" class="erro">{{ erros.email }}</p>

        <input v-model="form.endereco" type="text" placeholder="Seu endereço" />
        <p v-if="erros.endereco" class="erro">{{ erros.endereco }}</p>

        <button @click="finalizarCompra" class="btn-finalizar">Finalizar Compra</button>
      </div>

      <div v-if="mostrarModal" class="modal-overlay">
        <div class="modal">
          <h2>✅ Pedido Realizado!</h2>
          <p>Obrigado, <strong>{{ form.nome }}</strong>! Seu pedido foi recebido.</p>
          <button @click="fecharModal" class="btn-finalizar">Voltar à Loja</button>
        </div>
      </div>
    </div>

    <div v-else class="carrinho-vazio">
      <p>Seu carrinho está vazio </p>
      <RouterLink to="/produtos" class="btn-voltar">Ver Produtos</RouterLink>
    </div>
  </div>
</template>

<script>
import CartItem from '../components/carrinho/CartItem.vue'

export default {
  name: 'CarrinhoView',
  components: {
    CartItem
  },
  props: {
    carrinho: {
      type: Array,
      default: () => []
    }
  },
  emits: ['remover'],
  data() {
    return {
      mostrarModal: false,
      form: {
        nome: '',
        email: '',
        endereco: ''
      },
      erros: {
        nome: '',
        email: '',
        endereco: ''
      }
    }
  },
  computed: {
    total() {
      return this.carrinho.reduce((acc, item) => acc + item.preco * item.quantidade, 0)
    }
  },
  methods: {
    finalizarCompra() {
      this.erros = { nome: '', email: '', endereco: '' }
      let valido = true

      if (!this.form.nome.trim()) {
        this.erros.nome = 'Nome é obrigatório.'
        valido = false
      }
      if (!this.form.email.includes('@')) {
        this.erros.email = 'E-mail inválido.'
        valido = false
      }
      if (!this.form.endereco.trim()) {
        this.erros.endereco = 'Endereço é obrigatório.'
        valido = false
      }

      if (valido) {
        this.mostrarModal = true
      }
    },
    fecharModal() {
      this.mostrarModal = false
      this.$router.push('/produtos')
    }
  }
}
</script>

<style scoped>
.carrinho-page {
  padding: 32px;
  max-width: 800px;
  margin: 0 auto;
}

.carrinho-page h1 {
  font-size: 2rem;
  margin-bottom: 24px;
}

.carrinho-total {
  text-align: right;
  margin: 24px 0;
  font-size: 1.2rem;
}

.formulario {
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.formulario h2 {
  margin-bottom: 8px;
}

.formulario input {
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1rem;
}

.erro {
  color: #e74c3c;
  font-size: 0.85rem;
  margin-top: -8px;
}

.btn-finalizar {
  background-color: #2ecc71;
  color: white;
  border: none;
  padding: 14px;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
  transition: 0.3s;
}

.btn-finalizar:hover {
  background-color: #27ae60;
}

.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 999;
}

.modal {
  background: white;
  border-radius: 16px;
  padding: 40px;
  text-align: center;
  max-width: 400px;
  width: 90%;
}

.modal h2 {
  font-size: 1.8rem;
  margin-bottom: 16px;
}

.modal p {
  margin-bottom: 24px;
  font-size: 1rem;
}

.carrinho-vazio {
  text-align: center;
  margin-top: 80px;
}

.carrinho-vazio p {
  font-size: 1.3rem;
  margin-bottom: 24px;
  color: #888;
}

.btn-voltar {
  background-color: #3498db;
  color: white;
  padding: 12px 32px;
  border-radius: 8px;
  font-size: 1rem;
}
</style>