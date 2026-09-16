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
      <div>
        <input type="checkbox" id="item1" />
        <label for="item1"> Nokia </label>
      </div>

      <div>
        <input type="checkbox" id="item2" />
        <label for="item2"> Consul </label>
      </div>
      <div>
        <input type="checkbox" id="item3" />
        <label for="item2"> Dell </label>
      </div>

      <div>
        <input type="checkbox" id="item3" />
        <label for="item2"> Confort </label>
      </div>

      <h5 class="title-filter">Por categoria </h5>
      <div>
        <input type="checkbox" id="cat1" />
        <label for="cat1"> Eletrônicos </label>
      </div>
      <div>
        <input type="checkbox" id="cat2" />
        <label for="cat2"> Informática </label>
      </div>

      <div>
        <input type="checkbox" id="cat3" />
        <label for="cat2"> Moda </label>
      </div>
 
    </div>

    <div>
      <p>Quantidade encontrada: {{ filtrados.length }}</p> <br/>

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
    <button>
      <img src="https://img.icons8.com/ios-filled/50/double-left.png" alt="double-left" />
    </button>
    <span>1/5</span>
    <button>
      <img src="https://img.icons8.com/ios-filled/50/double-right.png" alt="double-left" />
    </button>
  </footer>
</template>

<script setup> 
import { ref,computed } from 'vue';
const modalCarrinho = ref(false);
const termoBusca = ref('');
const filtrarPor = ref('');
const submenuNavbar = ref(true);
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


