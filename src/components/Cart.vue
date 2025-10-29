<template>
  <div>
    <div
      class="backdrop"
      v-if="show"
      @click="$emit('close')"
    ></div>
    <aside :class="['cart-panel', { open: show }]">
      <header class="cart-header">
        <h3>Tu carrito</h3>
        <button class="close-btn" @click="$emit('close')">✕</button>
      </header>
      <div class="cart-content" v-if="items.length > 0">
        <div
          class="cart-item"
          v-for="item in items"
          :key="item.id"
        >
          <img :src="item.image" :alt="item.name" class="item-thumb" />
          <div class="item-info">
            <p class="item-name">{{ item.name }}</p>
            <p class="item-qty">Cantidad: {{ item.qty }}</p>
            <p class="item-price">$ {{ item.price.toLocaleString() }}</p>
          </div>
          <button
            class="remove-btn"
            @click="removeFromCart(item.id)"
            title="Eliminar"
          >
            🗑️
          </button>
        </div>
        <div class="cart-summary">
          <p>Total: <strong>$ {{ total.toLocaleString() }}</strong></p>
          <button class="checkout-btn">Proceder al pago</button>
        </div>
      </div>
      <div v-else class="empty-cart">
        <p>Tu carrito está vacío</p>
      </div>
    </aside>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useCartStore } from '../store/cartStore'

const props = defineProps({
  show: {
    type: Boolean,
    default: false
  }
})

const cartStore = useCartStore()

const items = computed(() => cartStore.items)
const total = computed(() => cartStore.total)

function removeFromCart (id) {
  cartStore.removeFromCart(id)
}
</script>

<style scoped>
.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3);
  z-index: 90;
}

.cart-panel {
  position: fixed;
  top: 0;
  right: 0;
  width: 320px;
  height: 100vh;
  background-color: var(--secondary-color);
  box-shadow: -2px 0 4px rgba(0, 0, 0, 0.1);
  z-index: 100;
  transform: translateX(100%);
  transition: transform 0.3s ease;
  display: flex;
  flex-direction: column;
}
.cart-panel.open {
  transform: translateX(0);
}

.cart-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  border-bottom: 1px solid var(--light-gray);
}
.cart-header h3 {
  margin: 0;
  font-size: 1.2rem;
}
.close-btn {
  background: none;
  border: none;
  font-size: 1.2rem;
}

.cart-content {
  flex-grow: 1;
  overflow-y: auto;
  padding: 1rem;
}

.cart-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.75rem;
}
.item-thumb {
  width: 50px;
  height: 50px;
  object-fit: cover;
  border-radius: 4px;
}
.item-info {
  flex-grow: 1;
}
.remove-btn {
  background: none;
  border: none;
  font-size: 1.1rem;
}
.cart-summary {
  margin-top: 1rem;
  border-top: 1px solid var(--light-gray);
  padding-top: 1rem;
}
.checkout-btn {
  width: 100%;
  margin-top: 0.5rem;
  padding: 0.5rem;
  background-color: var(--primary-color);
  color: #fff;
  border-radius: 4px;
}

.empty-cart {
  padding: 2rem;
  text-align: center;
  flex-grow: 1;
}
</style>