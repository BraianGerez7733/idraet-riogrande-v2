<template>
  <div class="product-detail" v-if="product">
    <div class="detail-container">
      <div class="image-box">
        <img :src="product.image" :alt="product.name" />
      </div>
      <div class="info-box">
        <h2>{{ product.name }}</h2>
        <p class="price">$ {{ product.price.toLocaleString() }}</p>
        <button class="buy-btn" @click="addToCart">Comprar</button>
        <div class="section">
          <h3>Descripción</h3>
          <p>{{ product.description }}</p>
        </div>
        <div class="section" v-if="product.benefits">
          <h3>Beneficios</h3>
          <p>{{ product.benefits }}</p>
        </div>
        <div class="section" v-if="product.ingredients">
          <h3>Ingredientes</h3>
          <p>{{ product.ingredients }}</p>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="loading">
    Cargando...
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import { useCartStore } from '../store/cartStore'

const route = useRoute()
const cartStore = useCartStore()

const product = ref(null)

onMounted(async () => {
  const res = await fetch('/data/products.json')
  const list = await res.json()
  product.value = list.find(item => item.id.toString() === route.params.id)
})

function addToCart () {
  if (product.value) {
    cartStore.addToCart(product.value)
    alert('Producto agregado al carrito')
  }
}
</script>

<style scoped>
.product-detail {
  padding: 1rem;
}

.detail-container {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
}

.image-box {
  flex: 1 1 300px;
}

.image-box img {
  width: 100%;
  border-radius: 8px;
  object-fit: cover;
}

.info-box {
  flex: 1 1 300px;
}

.price {
  font-size: 1.4rem;
  font-weight: 600;
  margin: 0.5rem 0;
}

.buy-btn {
  background-color: var(--primary-color);
  color: #fff;
  border: none;
  padding: 0.6rem 1.2rem;
  border-radius: 4px;
  margin-bottom: 1rem;
}

.section {
  margin-bottom: 1rem;
}

.section h3 {
  margin-bottom: 0.5rem;
  color: var(--primary-color);
}

.loading {
  padding: 2rem;
  text-align: center;
}

@media (max-width: 768px) {
  .detail-container {
    flex-direction: column;
  }
}
</style>