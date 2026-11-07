<script setup>
import { ref, computed } from 'vue'
import ProductCard from './components/ProductCard.vue'

import fone from './assets/products/fone.svg'
import teclado from './assets/products/teclado.svg'
import mouse from './assets/products/mouse.svg'
import monitor from './assets/products/monitor.svg'
import webcam from './assets/products/webcam.svg'
import relogio from './assets/products/relogio.svg'
import caixa from './assets/products/caixa.svg'
import ssd from './assets/products/ssd.svg'

const products = [
  { id: 1, name: 'Fone de Ouvido Bluetooth', price: 249.9, image: fone },
  { id: 2, name: 'Teclado Mecânico', price: 329.0, image: teclado },
  { id: 3, name: 'Mouse Gamer Sem Fio', price: 159.9, image: mouse },
  { id: 4, name: 'Monitor 24" Full HD', price: 899.0, image: monitor },
  { id: 5, name: 'Webcam Full HD', price: 189.5, image: webcam },
  { id: 6, name: 'Smartwatch Fitness', price: 399.9, image: relogio },
  { id: 7, name: 'Caixa de Som Portátil', price: 219.0, image: caixa },
  { id: 8, name: 'SSD 480GB', price: 279.9, image: ssd },
]

// Estado reativo (Requisitos 2 e 3)
const cartCount = ref(0)
const search = ref('')

// Lista filtrada em tempo real, ignorando maiúsculas e acentos.
const normalize = (text) =>
  text.normalize('NFD').replace(/[̀-ͯ]/g, '').toLowerCase()

const filteredProducts = computed(() => {
  const term = normalize(search.value.trim())
  return products.filter((p) => normalize(p.name).includes(term))
})

function addToCart() {
  cartCount.value++
}
</script>

<template>
  <header class="header">
    <div class="container header__inner">
      <h1 class="header__title">Catálogo Tech</h1>
      <p class="cart" role="status" aria-live="polite">
        <svg viewBox="0 0 24 24" width="22" height="22" aria-hidden="true" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="9" cy="20" r="1.5" />
          <circle cx="18" cy="20" r="1.5" />
          <path d="M2 3h3l2.7 12.4a1 1 0 0 0 1 .8h8.9a1 1 0 0 0 1-.8L20 7H6" />
        </svg>
        Itens no carrinho: <strong data-testid="cart-count">{{ cartCount }}</strong>
      </p>
    </div>
  </header>

  <main class="container">
    <div class="search">
      <label class="search__label" for="search">Buscar produto</label>
      <input
        id="search"
        v-model="search"
        class="search__input"
        type="search"
        placeholder="Digite o nome do produto..."
        autocomplete="off"
      />
    </div>

    <p class="results" aria-live="polite">
      {{ filteredProducts.length }}
      {{ filteredProducts.length === 1 ? 'produto encontrado' : 'produtos encontrados' }}
    </p>

    <section v-if="filteredProducts.length" class="grid" aria-label="Lista de produtos">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :name="product.name"
        :price="product.price"
        :image="product.image"
        @add-to-cart="addToCart"
      />
    </section>
    <p v-else class="empty">Nenhum produto encontrado para “{{ search }}”.</p>
  </main>
</template>

<style scoped>
.header {
  background: var(--color-primary);
  color: var(--color-on-primary);
  position: sticky;
  top: 0;
  z-index: 10;
}
.header__inner {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 8px 16px;
  padding-block: 16px;
}
.header__title {
  margin: 0;
  font-family: var(--font-heading);
  font-size: 1.5rem;
}
.cart {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin: 0;
  padding: 8px 14px;
  border-radius: 999px;
  background: rgb(255 255 255 / 0.16);
  font-weight: 500;
}
.cart strong {
  min-width: 1.2ch;
  text-align: center;
  font-size: 1.1rem;
}
.search {
  margin-block: 24px 8px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.search__label {
  font-weight: 600;
}
.search__input {
  width: 100%;
  min-height: 48px;
  padding: 10px 14px;
  font: inherit;
  color: var(--color-foreground);
  background: var(--color-card);
  border: 2px solid var(--color-border);
  border-radius: 10px;
}
.search__input:focus-visible {
  outline: 3px solid var(--color-ring);
  outline-offset: 2px;
  border-color: var(--color-accent);
}
.results {
  margin: 0 0 16px;
  color: var(--color-muted-foreground);
  font-size: 0.95rem;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 20px;
  padding-bottom: 48px;
}
.empty {
  padding: 48px 16px;
  text-align: center;
  color: var(--color-muted-foreground);
}
@media (max-width: 480px) {
  .header__inner {
    justify-content: center;
    text-align: center;
  }
  .grid {
    grid-template-columns: 1fr;
  }
}
</style>
