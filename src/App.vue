<script setup>
import { ref } from 'vue'
import CButton from './components/CButton.vue'
</script>

<script src="https://cdn.jsdelivr.net/npm/vue@3/dist/vue.global.js"></script>                
<script>
    const options = {
        data () {
            return {
                products: [],
                selected_product_id: null,

            }
        },
        computed: {
            selected_product() {
                return this.products.find ( product => {
                    return product.id == this.selected_product_id;
                })
            }
        },  
        methods: {
            setSelectedProduct(id) {
                this.selected_product_id = id;
            }
        },
        mounted() {
            fetch('https://api.escuelajs.co/api/v1/products?offset=0&limit=4')
                .then(res=>res.json())
                .then(json=> this.products = json);
        },
    };
    Vue.createApp(options).mount('#vue-app');
</script>

<div class="product-search">
  <template v-if="products.length > 0" v-for="(product, index) in products">
      <div class="product-card" 
      v-if="index < 4" @click="setSelectedProduct(product.id)">
          <img class="product-image" :src="product.images[0]">
          <div class="product-title" v-html="product.title"></div>
      </div>
  </template>
  <div v-else>Loading...</div>
  </div>

  <div v-if="selected_product" class="drawer" aria-hidden="false">
      <img :src="selected_product.images[0]">
      <div class="product-info">
          <h1 class="text-5xl font-bold mb-2" v-html="selected_product.title"></h1>
          <div class="price" v-html="'$'+selected_product.price"></div>
          <div v-html="selected_product.description"></div>
      </div>
  </div>


<template>
  <div>
    <h1>New Products</h1>
    <CButton>Click Me</CButton> 
    <div class="product-image" id="open-drawer-button">`this.product.image`</div> 
    <div class="prduct-name">`this.product.name`</div>
  </div>
</template>
