<template>
  <div>
    <Header @open-cart="openCart" />
    <main class="main-content">
      <router-view />
    </main>
    <Cart :show="cartVisible" @close="cartVisible = false" />
    <Footer />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Cart from './components/Cart.vue'

const cartVisible = ref(false)

function openCart () {
  cartVisible.value = true
}
</script>

<style scoped>
.main-content {
  padding-top: 140px; /* space for fixed header and banner */
}
</style>