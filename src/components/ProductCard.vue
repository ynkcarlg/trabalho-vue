<script setup>
import { computed } from 'vue'

// Requisito 1: nome, preço e imagem chegam por props.
const props = defineProps({
  name: { type: String, required: true },
  price: { type: Number, required: true },
  image: { type: String, required: true },
})

// Requisito 2: o card avisa o componente pai via evento.
const emit = defineEmits(['add-to-cart'])

const formattedPrice = computed(() =>
  props.price.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }),
)

function addToCart() {
  emit('add-to-cart', props.name)
}
</script>

<template>
  <article class="card">
    <img class="card__image" :src="image" :alt="name" loading="lazy" />
    <div class="card__body">
      <h2 class="card__name">{{ name }}</h2>
      <p class="card__price">{{ formattedPrice }}</p>
      <button class="card__button" type="button" @click="addToCart">
        <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="9" cy="20" r="1.5" />
          <circle cx="18" cy="20" r="1.5" />
          <path d="M2 3h3l2.7 12.4a1 1 0 0 0 1 .8h8.9a1 1 0 0 0 1-.8L20 7H6" />
        </svg>
        Adicionar ao Carrinho
      </button>
    </div>
  </article>
</template>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  background: var(--color-card);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  overflow: hidden;
  transition: border-color 0.18s ease, transform 0.18s ease;
}
.card:hover {
  border-color: var(--color-accent);
  transform: translateY(-2px);
}
.card__image {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
  display: block;
}
.card__body {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding: 16px;
  flex: 1;
}
.card__name {
  font-size: 1.05rem;
  font-weight: 600;
  color: var(--color-foreground);
  margin: 0;
}
.card__price {
  font-family: var(--font-heading);
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--color-primary);
  margin: 0 0 8px;
}
.card__button {
  margin-top: auto;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  min-height: 44px;
  padding: 10px 16px;
  border: 0;
  border-radius: 8px;
  background: var(--color-accent);
  color: var(--color-on-accent);
  font: inherit;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.18s ease, transform 0.1s ease;
}
.card__button:hover {
  background: var(--color-accent-hover);
}
.card__button:active {
  transform: scale(0.98);
}
.card__button:focus-visible {
  outline: 3px solid var(--color-ring);
  outline-offset: 2px;
}
@media (prefers-reduced-motion: reduce) {
  .card,
  .card__button {
    transition: none;
  }
  .card:hover {
    transform: none;
  }
}
</style>
