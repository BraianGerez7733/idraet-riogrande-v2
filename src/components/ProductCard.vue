<template>
  <div class="product-card">
    <div class="image-wrapper">
      <router-link :to="`/product/${product.id}`">
        <img :src="product.image" :alt="product.name" />
      </router-link>
      <div class="badges">
        <span
          v-for="badge in product.tags"
          :key="badge"
          class="badge"
        >
          {{ badge }}
        </span>
      </div>
    </div>
    <h4 class="product-name">
      <router-link :to="`/product/${product.id}`">
        {{ product.name }}
      </router-link>
    </h4>
    <p class="product-price">$ {{ product.price.toLocaleString() }}</p>
    <button class="add-button" @click="$emit('add', product)">
      Agregar al carrito
    </button>
  </div>
</template>

<script setup>
defineProps({
  product: {
    type: Object,
    required: true
  }
})
</script>

<style scoped>
.product-card {
  background-color: var(--secondary-color);
  border: 1px solid var(--light-gray);
  border-radius: 8px;
  padding: 0.75rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.image-wrapper {
  position: relative;
}
.image-wrapper img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 6px;
}

.badges {
  position: absolute;
  top: 8px;
  left: 8px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.badge {
  background-color: var(--primary-color);
  color: #fff;
  font-size: 0.65rem;
  padding: 2px 6px;
  border-radius: 4px;
}

.product-name {
  margin: 0.75rem 0 0.25rem;
  font-size: 1rem;
}

.product-price {
  font-weight: 600;
  margin: 0 0 0.75rem;
}

.add-button {
  align-self: flex-start;
  background-color: var(--primary-color);
  color: #fff;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-size: 0.85rem;
}
</style>