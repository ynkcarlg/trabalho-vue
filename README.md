# Catálogo Tech — Vue.js 3

Projeto prático da disciplina de Programação Web I (Engenharia de Software): um catálogo de produtos com carrinho de compras, feito para demonstrar reatividade, data binding, props, eventos e componentização no Vue 3.

## Tecnologias

- [Vue 3](https://vuejs.org/) (Composition API com `<script setup>`)
- [Vite](https://vite.dev/)
- HTML, CSS (variáveis CSS, grid, media queries)

## Funcionalidades

- **Card de produto reutilizável** (`ProductCard.vue`): recebe `name`, `price` e `image` por **props** e exibe o botão "Adicionar ao Carrinho".
- **Evento para o componente pai**: o clique emite `add-to-cart`; o `App.vue` incrementa o contador sem recarregar a página ("Itens no carrinho: 0, 1, 2...").
- **Busca em tempo real**: campo com `v-model` e lista filtrada por `computed` (ignora maiúsculas e acentos).
- **Interface responsiva**: grid que se adapta a celular, tablet e desktop, foco visível no teclado, `aria-live` no contador e respeito a `prefers-reduced-motion`.

## Estrutura

```
catalogo-vue/
├── src/
│   ├── components/
│   │   └── ProductCard.vue
│   ├── assets/products/   (imagens SVG dos produtos)
│   ├── App.vue
│   ├── main.js
│   └── style.css
├── index.html
├── package.json
└── README.md
```

## Como executar

Requer Node.js 18 ou superior.

```bash
npm install
npm run dev
```

Abra o endereço exibido no terminal (normalmente http://localhost:5173).

Para gerar a versão de produção: `npm run build`.
