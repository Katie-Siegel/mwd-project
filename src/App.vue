<script setup>
import { ref } from 'vue'
import CButton from './components/CButton.vue'


const count = ref(0)
</script>

<template>
  <div>
    <h1>New Products</h1>
    <CButton>Click Me</CButton> 
    <div class="product-image" @click="drawer.hidden=false">`this.product.image`</div> 
    <div class="prduct-name">`this.product.name`</div>
  </div>
</template>
