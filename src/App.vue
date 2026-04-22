<script setup>
import { ref, computed, onMounted } from 'vue'
import'./main.js'
const products = ref([])
const selected_product_id = ref(null)

const selected_product = computed(() => {
  return products.value.find(product => product.id === selected_product_id.value)
})

function setSelectedProduct(id) {
  selected_product_id.value = id
}

onMounted(async () => {
  const res = await fetch('https://api.escuelajs.co/api/v1/products?offset=0&limit=20')
  products.value = await res.json()
})
</script>

<template>
  <div class="template-container">
    <h1>New Products</h1>
    <div class="product-search">
      <div v-if="products.length > 0">
        <div 
          v-for="product in products" 
          :key="product.id"
          class="product-card"
          @click="setSelectedProduct(product.id)"
        >
          <img class="product-image" :src="product.images[0]" />
          <div class="product-title">{{ product.title }}</div>
        </div>
      </div>
      <div v-else>Loading...</div>
    </div>

    <div v-if="selected_product" class="drawer">
      <img :src="selected_product.images[0]" />
      <div class="product-info">
        <h1>{{ selected_product.title }}</h1>
        <h3 class="price">Price: ${{ selected_product.price }}</h3>
        <div>{{ selected_product.description }}</div>
        <button class="close-drawer-button" @click="selected_product_id = null">Back to Search</button>
      </div>
    </div>
  </div>
</template>
