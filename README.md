# 🛍️ LojaVue

Projeto desenvolvido para a disciplina de Front-End utilizando Vue.js.

## 👥 Integrantes do Grupo

- Gabriel Goes
- Matheus Henrique Ferreira
- Gustavo Ribas

## 🛠️ Tecnologias Utilizadas

- Vue.js 3
- Vue Router
- Vite
- HTML5
- CSS3
- JavaScript

## ⚙️ Como Executar o Projeto

### Pré-requisitos

- Node.js instalado (https://nodejs.org)
- Git instalado (https://git-scm.com)

### Passo a passo

1. Clone o repositório:
 git clone https://github.com/GabrielGoesDev13/loja-vue.git

 2. Entre na pasta do projeto:
cd loja-vue

3. Instale as dependências:
npm install

4. Inicie o servidor de desenvolvimento:
npm run dev

5. Acesse no navegador:
http://localhost:5173

## 📁 Estrutura do Projeto
src/
├── components/
│    carrinho/
│   │CartItem.vue
│    layout/
│   │ NavBar.vue
│   └produtos/
│      └ProductCard.vue
├── router/
│   index.js
├── views/
│   CarrinhoView.vue
│   HomeView.vue
│   ProdutosView.vue
├── App.vue
└── main.js

## ✅ Funcionalidades

- Página Home com banner e categorias
- Lista de produtos com busca e filtro por categoria
- Carrinho de compras com adicionar e remover itens
- Formulário de finalizar compra com validação de campos
- Modal de confirmação de pedido
- Interface responsiva 