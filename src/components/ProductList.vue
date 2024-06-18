<template>
  <div>
    <SearchBar :categories="categories" @category-selected="filterProductsByCategory" />
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
      <ProductCard 
        v-for="product in filteredProducts" 
        :key="product.id" 
        :product="product"
        @click="selectProduct(product.id)"
        @add-to-cart="addToCart(product)"
      />
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import ProductCard from './ProductCard.vue'
import SearchBar from './SearchBar.vue'

export default {
  components: {
    ProductCard,
    SearchBar,
  },
  emits: ['select-product', 'add-to-cart'],
  setup(_, { emit }) {
    const products = ref([])
    const filteredProducts = ref([])
    const categories = ref([])

    onMounted(async () => {
      await fetchProducts()
      await fetchCategories()
    })

    const fetchProducts = async () => {
      const res = await fetch('https://fakestoreapi.com/products')
      const data = await res.json()
      products.value = data
      filteredProducts.value = data
    }

    const fetchCategories = async () => {
      const res = await fetch('https://fakestoreapi.com/products/categories')
      const data = await res.json()
      categories.value = data
    }

    const filterProductsByCategory = (category) => {
      if (category === "") {
        filteredProducts.value = products.value
      } else {
        filteredProducts.value = products.value.filter(product => product.category === category)
      }
    }

    const selectProduct = (productId) => {
      emit('select-product', productId)
    }

    const addToCart = (product) => {
      emit('add-to-cart', product)
    }

    return {
      products,
      filteredProducts,
      categories,
      fetchProducts,
      fetchCategories,
      filterProductsByCategory,
      selectProduct,
      addToCart,
    }
  },
}
</script>
