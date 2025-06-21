<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Noble Tech | Loja Online</title>
  <script src="https://unpkg.com/vue@3"></script>
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f4f4f4;
    }
    header {
      background-color: #222;
      color: #fff;
      padding: 1rem;
      text-align: center;
    }
    .produtos {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1rem;
      padding: 2rem;
    }
    .produto {
      background: #fff;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      text-align: center;
    }
    .produto img {
      max-width: 100%;
      height: auto;
    }
    .botao-whats {
      display: inline-block;
      margin-top: 1rem;
      padding: 0.5rem 1rem;
      background-color: #25D366;
      color: #fff;
      border: none;
      border-radius: 5px;
      text-decoration: none;
    }
    .carrinho {
      position: fixed;
      top: 1rem;
      right: 1rem;
      background: #fff;
      border: 1px solid #ccc;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    footer {
      background: #222;
      color: #fff;
      text-align: center;
      padding: 1rem;
    }
  </style>
</head>
<body>
  <div id="app">
    <header>
      <h1>Noble Tech</h1>
      <p>Acessórios para Celular e Assistência Técnica</p>
    </header>

    <section class="produtos">
      <div class="produto" v-for="produto in produtos" :key="produto.id">
        <img :src="produto.imagem" :alt="produto.nome">
        <h2>{{ produto.nome }}</h2>
        <p>R$ {{ produto.preco.toFixed(2) }}</p>
        <button class="botao-whats" @click="adicionarAoCarrinho(produto)">Adicionar ao Carrinho</button>
      </div>
    </section>

    <div class="carrinho" v-if="carrinho.length">
      <h3>Carrinho</h3>
      <ul>
        <li v-for="item in carrinho">{{ item.nome }} - R$ {{ item.preco.toFixed(2) }}</li>
      </ul>
      <p><strong>Total:</strong> R$ {{ totalCarrinho.toFixed(2) }}</p>
      <a class="botao-whats" :href="linkWhatsapp" target="_blank">Finalizar Pedido no WhatsApp</a>
    </div>

    <footer>
      <p>&copy; 2025 Noble Tech - Todos os direitos reservados.</p>
    </footer>
  </div>

  <script>
    const { createApp } = Vue;
    createApp({
      data() {
        return {
          produtos: [
            { id: 1, nome: 'Capinha para Celular', preco: 29.90, imagem: 'https://via.placeholder.com/200x200' },
            { id: 2, nome: 'Película de Vidro', preco: 19.90, imagem: 'https://via.placeholder.com/200x200' },
            { id: 3, nome: 'Carregador Turbo', preco: 59.90, imagem: 'https://via.placeholder.com/200x200' },
          ],
          carrinho: [],
        }
      },
      computed: {
        totalCarrinho() {
          return this.carrinho.reduce((total, item) => total + item.preco, 0);
        },
        linkWhatsapp() {
          const numero = '5591999999999';
          const texto = encodeURIComponent('Olá! Gostaria de fazer o seguinte pedido:\n' + this.carrinho.map(p => `- ${p.nome} (R$ ${p.preco.toFixed(2)})`).join('\n') + `\nTotal: R$ ${this.totalCarrinho.toFixed(2)}`);
          return `https://wa.me/${numero}?text=${texto}`;
        }
      },
      methods: {
        adicionarAoCarrinho(produto) {
          this.carrinho.push(produto);
        }
      }
    }).mount('#app')
  </script>
</body>
</html>
