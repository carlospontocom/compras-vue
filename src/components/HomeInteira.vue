<template>
  <header>
  <div class="header-content">
    <div class="logomarca">
      <img src="https://img.icons8.com/3d-fluency/94/shopping-basket.png" alt="shopping-basket" />
      <div class="logo-text">
        Compras.vue
      </div>
    </div>

    <input type="text" placeholder="Digite sua busca" class="field-search" v-model="termoBusca">

    <div>
      <img width="24" height="24" src="https://img.icons8.com/material-outlined/24/shopping-cart--v1.png" alt="icone carrinho de compras"/>
      <span>Carrinho</span>
    </div>

    <img width="24" height="24" src="https://img.icons8.com/material-outlined/24/user--v1.png" alt="user--v1"/>
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

<style scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

ul {
  list-style: none;
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}


.container{
  border:4px solid green;
  max-width: 1024px;
  width:100%;
  margin: 0 auto;
}

@media (min-width: 500px) {
  ul {
    list-style: none;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
  }
}

.cards-vitrine{
  display: flex;
  flex-wrap: wrap;
  gap:1rem;
}

.card {
  border: 1px solid #ccc;
  padding: 1rem;
  border-radius: 3px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-height: 150px;
  flex: 1 1 180px;
}

ul li button {
  margin-top: auto;
}

.header-content {
  display: flex;
  position:fixed;
  top: 0;
  left: 0;
  z-index: 200;
  background-color: white;
  box-shadow: 0 0 10px #00000050;
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 3rem;
  padding: 8px;
 }

.logomarca {
  display: flex;
  align-items: center;
}

.logomarca img {
  width: 50px;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: bold;
}

.field-search {
  padding: .6rem 5px;
  width: 50%;
}

.vitrine-online {
  display: grid;
  grid-template-columns: 1fr 2fr;
  padding: 5.6rem 1rem;
}

.aside-filter {
  background: rgb(231, 219, 219, .4);
  padding: 0 2rem;
  min-height: 100vh;
}

.title-filter {
  font-size: 1.1rem;
  padding: 1rem 0;
}

.btn-comprar {
  background-color: seagreen;
  color: white;
  cursor: pointer;
  border: 0;
  padding: 10px;
}

.carrinho-compras {
  background-color: #f2f2f2;
  position: fixed;
  z-index: 10;
  top: 3.4rem;
  right: 0;
  width: 100%;
  max-width: 320px;
  height: 100vh;
}

.footer-pagination {
  background-color: #f2f2f2;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.footer-pagination span {
  font-size: 1.5rem;
}

.footer-pagination button img {
  width: 33px;
}

.footer-pagination button {
  border: 0;
  cursor: pointer;
  background-color: slategray;
}

.carrinho-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid #ccc;
  padding: 1rem;
}

.carrinho-content {
  padding: 1rem;
}

.fechar-carrinho {
  background-color: tomato;
  font-size: 2rem;
  padding: 0 .6rem;
  border: 0;
  color: white;
  cursor: pointer;
  border-radius: 4px;
}
</style>
