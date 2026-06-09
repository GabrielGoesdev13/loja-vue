<template>
  <div class="home">
    <!-- Banner principal -->
    <section class="banner">
      <h1>Bem-vindo à LojaVue 🛍️</h1>
      <p>Os melhores produtos com os melhores preços!</p>
      <RouterLink to="/produtos" class="btn-banner">Ver Produtos</RouterLink>
    </section>

    <!-- Seção de categorias -->
    <section class="categorias">
      <h2>Categorias</h2>
      <div class="categorias-grid">
        <div v-for="categoria in categorias" :key="categoria.id" class="categoria-card">
          <span class="categoria-icone">{{ categoria.icone }}</span>
          <p>{{ categoria.nome }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'HomeView',
  data() {
    return {
      categorias: [
        { id: 1, nome: 'Eletrônicos', icone: '💻' },
        { id: 2, nome: 'Roupas', icone: '👕' },
        { id: 3, nome: 'Calçados', icone: '👟' },
        { id: 4, nome: 'Acessórios', icone: '⌚' }
      ]
    }
  }
}
</script>

<style scoped>
.banner {
  background: linear-gradient(135deg, #2c3e50, #3498db);
  color: white;
  text-align: center;
  padding: 80px 32px;
}

.banner h1 {
  font-size: 2.5rem;
  margin-bottom: 16px;
}

.banner p {
  font-size: 1.2rem;
  margin-bottom: 32px;
}

.btn-banner {
  background-color: #fff;
  color: #2c3e50;
  padding: 12px 32px;
  border-radius: 30px;
  font-weight: bold;
  font-size: 1rem;
  transition: 0.3s;
}

.btn-banner:hover {
  background-color: #3498db;
  color: white;
}

.categorias {
  padding: 48px 32px;
  text-align: center;
}

.categorias h2 {
  font-size: 1.8rem;
  margin-bottom: 32px;
}

.categorias-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 24px;
  max-width: 800px;
  margin: 0 auto;
}

.categoria-card {
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: 0.3s;
  cursor: pointer;
}

.categoria-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 16px rgba(0,0,0,0.15);
}

.categoria-icone {
  font-size: 2.5rem;
}

.categoria-card p {
  margin-top: 12px;
  font-weight: bold;
}
</style>