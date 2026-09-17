<template>
  <header>
  <div class="header-content">
    <div class="logomarca">
      <img src="https://img.icons8.com/3d-fluency/94/shopping-basket.png" alt="shopping-basket" />
      <p class="logo-text">
        Compras.vue
      </p>
    </div>

    <input type="text" placeholder="Digite sua busca" class="field-search" v-model="termoBusca">

    <div class="ddflex">
      <img width="24" height="24" src="https://img.icons8.com/material-outlined/24/shopping-cart--v1.png" alt="icone carrinho de compras"/>
      <span class="t-icone-cart">Carrinho</span>
    </div>

    <img width="24" height="24" src="https://img.icons8.com/material-outlined/24/user--v1.png" alt="user--v1" @click="submenuNavbar = !submenuNavbar" class="icone-user"/>

    
      <ul v-if="submenuNavbar" class="submenuNavbar">
        <li>carlos@gmail.com</li>
        <li>sair</li>
      </ul>
    </div>

  </header>

  <section class="vitrine-online">
    <div class="aside-filter">
      <h5 class="title-filter">Por marca</h5>
      <div class="sepador-item-checkbox">
        <input type="checkbox" id="nokia" />
        <label for="nokia"> Nokia </label>
      </div>

      <div class="sepador-item-checkbox">
        <input type="checkbox" id="consul" />
        <label for="consul"> Consul </label>
      </div>
      <div class="sepador-item-checkbox">
        <input type="checkbox" id="dell" />
        <label for="dell"> Dell </label>
      </div>

      <div class="sepador-item-checkbox">
        <input type="checkbox" id="confort" />
        <label for="confort"> Confort </label>
      </div>

      <h5 class="title-filter">Por categoria </h5>
      <div class="sepador-item-checkbox">
        <input type="checkbox" id="catEletronicos" />
        <label for="catEletronicos"> Eletrônicos </label>
      </div>
      <div class="sepador-item-checkbox">
        <input type="checkbox" id="catInformatica" />
        <label for="catInformatica"> Informática </label>
      </div>

      <div class="sepador-item-checkbox">
        <input type="checkbox" id="catModa" />
        <label for="catModa"> Moda </label>
      </div>

      <button class="btn-limpar-filter"> Limpar filtros</button>
 
    </div>

    <div>
      <p class="qtn-encontrada">Quantidade encontrada: {{ filtrados.length }}</p> <br/>

      <div class="cards-vitrine">
      <div v-for="item in filtrados" :key="item.id" class="card">
        <p>
          {{ item.item }}
        </p>
        <p>
          {{ item.valor }}
        </p>
        <button @click="abrirCarrinho" class="btn-comprar">Comprar</button>
      </div>
      </div>
    </div>


  </section>

  <div class="carrinho-compras" v-if="modalCarrinho">
    <div class="carrinho-header">
      <h4>Carrinho de compras</h4>
      <button @click="fecharCarrinho" class="fechar-carrinho">x</button>
    </div>

    <div class="carrinho-content">
      <div v-for="item in itemCarrinho" :key="item.id">
        {{ item.item }}
      </div>
    </div>
  </div>

  <footer class="footer-pagination">
    <button><<</button>
    <span>1/5</span>
    <button>>></button>
  </footer>
</template>

<script setup> 
import { ref,computed } from 'vue';
const modalCarrinho = ref(false);
const termoBusca = ref('');
const filtrarPor = ref('');
const submenuNavbar = ref(false);
import '@/css/home.css';

const filtrados = computed(()=>{
  return produtos.value.filter(i=>i.item.toLowerCase().includes(termoBusca.value.toLowerCase()))
})


const itemCarrinho = ref([
  {
    id: 12,
    item: "computador"
  }
]);

const produtos = ref([
  {
    id: 1,
    item: "computador",
    marca:"dell",
    categoria:"informática",
    valor: 4550
  },
  {
    id: 2,
    item: "celular",
    marca:"dell",
    categoria:"eletrônico",
    valor: 1600
  },
  {
    id: 3,
    item: "tablet",
    marca:"dell",
    categoria:"eletrônico",
    valor: 1200
  },
  {
    id: 4,
    item: "monitor",
    categoria:"informática",
    valor: 850
  },
  {
    id: 5,
    item: "teclado",
    marca:"dell",
    categoria:"informática",
    valor: 150
  },
  {
    id: 6,
    item: "camisa",
    marca:"confort",
    categoria:"",
    valor: 90
  },
  {
    id: 7,
    item: "tênis",
    marca:"confort",
    valor: 650
  },
  {
    id: 8,
    item: "notebook",
    marca:"consul",
    valor: 3800
  },
  {
    id: 9,
    item: "headset",
    marca:"consul",
    valor: 280
  },
  {
    id: 10,
    item: "webcam",
    marca:"dell",
    valor: 220
  }
]);

function abrirCarrinho() {
  modalCarrinho.value = true;
}

function fecharCarrinho() {
  modalCarrinho.value = false;
}

</script>


