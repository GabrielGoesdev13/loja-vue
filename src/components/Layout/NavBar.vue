<template>
  
  <nav class="navbar">
    <div class="navbar-logo">
      <RouterLink to="/">🛍️ LojaVue</RouterLink>
    </div>

    <div class="navbar-links">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/produtos">Produtos</RouterLink>
      <RouterLink to="/carrinho">
        🛒 Carrinho
       
        <span v-if="totalItens > 0" class="badge">{{ totalItens }}</span>
      </RouterLink>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  props: {
   
    totalItens: {
      type: Number,
      default: 0
    }
  }
}
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #2c3e50;
  padding: 16px 32px;
  position: sticky;
  top: 0;
  z-index: 100;
}

.navbar-logo a {
  color: #fff;
  font-size: 1.4rem;
  font-weight: bold;
  text-decoration: none;
}

.navbar-links {
  display: flex;
  gap: 24px;
}

.navbar-links a {
  color: #ecf0f1;
  text-decoration: none;
  font-size: 1rem;
  position: relative;
}

.navbar-links a:hover {
  color: #3498db;
}

.badge {
  background-color: #e74c3c;
  color: white;
  border-radius: 50%;
  padding: 2px 7px;
  font-size: 0.75rem;
  margin-left: 4px;
}


@media (max-width: 600px) {
  .navbar {
    flex-direction: column;
    gap: 12px;
  }
}
</style>