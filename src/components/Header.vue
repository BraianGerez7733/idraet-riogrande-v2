<template>
  <header class="site-header">
    <div class="top-bar">
      ENVÍOS GRATIS EN RÍO GRANDE A PARTIR DE $80.000
    </div>
    <div class="nav-bar">
      <div class="logo" @click="$router.push('/')">
        <div class="logo-circle">
          <span class="logo-title">IDRAET</span>
          <span class="logo-sub">Río Grande</span>
        </div>
      </div>
      <nav class="menu">
        <router-link to="/">Inicio</router-link>
        <router-link to="/">Productos</router-link>
        <router-link to="/">Contacto</router-link>
      </nav>
      <div class="actions">
        <!-- Search icon placeholder -->
        <button class="icon-btn" title="Buscar">
          🔍
        </button>
        <!-- User icon placeholder -->
        <button class="icon-btn" title="Usuario">
          👤
        </button>
        <!-- Cart icon -->
        <button class="icon-btn cart-btn" title="Carrito" @click="$emit('open-cart')">
          🛒
          <span v-if="cartCount > 0" class="cart-count">{{ cartCount }}</span>
        </button>
      </div>
    </div>
  </header>
</template>

<script setup>
import { computed } from 'vue'
import { useCartStore } from '../store/cartStore'

const cartStore = useCartStore()
const cartCount = computed(() => cartStore.count)
</script>

<style scoped>
.site-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background-color: var(--secondary-color);
  border-bottom: 1px solid var(--light-gray);
  z-index: 100;
}

.top-bar {
  background-color: var(--primary-color);
  color: #fff;
  text-align: center;
  padding: 0.25rem 0;
  font-size: 0.85rem;
  font-weight: 500;
}

.nav-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem 1rem;
}

.logo {
  cursor: pointer;
}

.logo-circle {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: var(--primary-color);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-weight: 600;
  text-align: center;
  font-size: 0.65rem;
  line-height: 1;
}

.logo-title {
  font-size: 0.75rem;
  font-weight: 600;
}

.logo-sub {
  font-size: 0.6rem;
}

.menu {
  display: flex;
  gap: 1rem;
  align-items: center;
  font-weight: 500;
}

.menu a {
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
}

.menu a:hover {
  background-color: var(--primary-color);
  color: #fff;
}

.actions {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.icon-btn {
  background: none;
  border: none;
  font-size: 1.1rem;
  position: relative;
}

.cart-btn {
  position: relative;
}

.cart-count {
  position: absolute;
  top: -6px;
  right: -10px;
  background: var(--primary-color);
  color: #fff;
  font-size: 0.6rem;
  padding: 0 4px;
  border-radius: 8px;
}
</style>