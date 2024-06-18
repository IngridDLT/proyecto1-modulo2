<template>
  <div class="container mx-auto p-4">
    <div class="flex justify-between items-center mb-4">
      <h1 class="text-4xl font-bold text-blue-800">Product Store</h1>
      <div class="flex items-center">
        <i 
          class="fa-solid fa-cart-shopping text-2xl cursor-pointer" 
          @click="toggleCart"
        ></i>
        <span class="ml-2 text-lg">{{ cartItems.length }}</span>
      </div>
    </div>
    <ProductList @select-product="fetchProductDetails" @add-to-cart="addToCart" />
    <ProductDetail :product="selectedProduct" v-if="selectedProduct" />
    <ShoppingCart v-if="showCart" :cartItems="cartItems" @remove-from-cart="removeFromCart" @close="toggleCart" />
  </div>
</template>

<script>
import { ref } from 'vue'
import ProductList from './components/ProductList.vue'
import ProductDetail from './components/ProductDetail.vue'
import ShoppingCart from './components/ShoppingCart.vue'

export default {
  components: {
    ProductList,
    ProductDetail,
    ShoppingCart,
  },
  setup() {
    const selectedProduct = ref(null)
    const cartItems = ref([])
    const showCart = ref(false)

    const fetchProductDetails = async (productId) => {
      const res = await fetch(`https://fakestoreapi.com/products/${productId}`)
      const data = await res.json()
      selectedProduct.value = data
    }

    const addToCart = (product) => {
      cartItems.value.push(product)
    }

    const removeFromCart = (productId) => {
      cartItems.value = cartItems.value.filter(item => item.id !== productId)
    }

    const toggleCart = () => {
      showCart.value = !showCart.value
    }

    return {
      selectedProduct,
      cartItems,
      showCart,
      fetchProductDetails,
      addToCart,
      removeFromCart,
      toggleCart,
    }
  },
}
</script>
