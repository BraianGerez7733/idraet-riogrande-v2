<template>
  <div class="home-view">
    <div class="layout">
      <aside class="sidebar">
        <h3>Categorías</h3>
        <ul>
          <li
            :class="{ active: selectedCategory === null }"
            @click="selectCategory(null)"
          >
            Todas
          </li>
          <li
            v-for="cat in categories"
            :key="cat"
            :class="{ active: selectedCategory === cat }"
            @click="selectCategory(cat)"
          >
            {{ cat }}
          </li>
        </ul>
      </aside>
      <section class="content">
        <div class="controls">
          <input
            type="text"
            v-model="searchTerm"
            placeholder="Buscar productos..."
            class="search-input"
          />
          <select v-model="sortOrder" class="sort-select">
            <option value="new">Más nuevo a más viejo</option>
            <option value="old">Más viejo a más nuevo</option>
            <option value="priceLow">Precio menor</option>
            <option value="priceHigh">Precio mayor</option>
          </select>
        </div>
        <div class="product-grid">
          <ProductCard
            v-for="product in filteredProducts"
            :key="product.id"
            :product="product"
            @add="addToCart"
          />
        </div>
        <!-- Video block -->
        <VideoBlock />
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import ProductCard from '../components/ProductCard.vue'
import VideoBlock from '../components/VideoBlock.vue'
import { useCartStore } from '../store/cartStore'

const products = ref([])
const selectedCategory = ref(null)
const searchTerm = ref('')
const sortOrder = ref('new')

const cartStore = useCartStore()

onMounted(async () => {
  const res = await fetch('/data/products.json')
  products.value = await res.json()
})

const categories = computed(() => {
  const set = new Set(products.value.map(p => p.category))
  return Array.from(set)
})

const filteredProducts = computed(() => {
  let list = products.value.slice()
  if (selectedCategory.value) {
    list = list.filter(item => item.category === selectedCategory.value)
  }
  if (searchTerm.value.trim().length > 0) {
    const term = searchTerm.value.toLowerCase()
    list = list.filter(item => item.name.toLowerCase().includes(term))
  }
  switch (sortOrder.value) {
    case 'priceLow':
      list.sort((a, b) => a.price - b.price)
      break
    case 'priceHigh':
      list.sort((a, b) => b.price - a.price)
      break
    case 'old':
      list.sort((a, b) => parseInt(a.id) - parseInt(b.id))
      break
    case 'new':
    default:
      list.sort((a, b) => parseInt(b.id) - parseInt(a.id))
      break
  }
  return list
})

function selectCategory (cat) {
  selectedCategory.value = cat
}
function addToCart (product) {
  cartStore.addToCart(product)
}
</script>

<style scoped>
.layout {
  display: flex;
}

.sidebar {
  width: 200px;
  padding: 1rem;
  background-color: var(--secondary-color);
  border-right: 1px solid var(--light-gray);
  height: 100%;
  position: sticky;
  top: 140px;
  max-height: calc(100vh - 140px);
  overflow-y: auto;
}

.sidebar h3 {
  margin-top: 0;
}

.sidebar ul li {
  padding: 0.4rem 0;
  cursor: pointer;
}

.sidebar ul li.active {
  font-weight: 600;
  color: var(--primary-color);
}

.content {
  flex: 1;
  padding: 1rem;
}

.controls {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
  align-items: center;
}

.search-input {
  flex-grow: 1;
  padding: 0.5rem;
  border: 1px solid var(--light-gray);
  border-radius: 4px;
}

.sort-select {
  padding: 0.5rem;
  border: 1px solid var(--light-gray);
  border-radius: 4px;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
}

@media (max-width: 768px) {
  .layout {
    flex-direction: column;
  }
  .sidebar {
    width: 100%;
    position: relative;
    top: auto;
    border-right: none;
    border-bottom: 1px solid var(--light-gray);
    max-height: none;
  }
}
</style>