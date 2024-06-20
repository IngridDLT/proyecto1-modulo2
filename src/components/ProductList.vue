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
import ProductCard from './ProductCard.vue'
import SearchBar from './SearchBar.vue'

export default {
  components: {
    ProductCard,
    SearchBar,
  },
  emits: ['select-product', 'add-to-cart'],
  data() {
    return {
      products: [],
      filteredProducts: [],
      categories: [],
    }
  },
  mounted() {
    this.fetchProducts()
    this.fetchCategories()
  },
  methods: {
    async fetchProducts() {
      const res = await fetch('https://fakestoreapi.com/products')
      const data = await res.json()
      this.products = data
      this.filteredProducts = data
    },
    async fetchCategories() {
      const res = await fetch('https://fakestoreapi.com/products/categories')
      const data = await res.json()
      this.categories = data
    },
    filterProductsByCategory(category) {
      if (category === "") {
        this.filteredProducts = this.products
      } else {
        this.filteredProducts = this.products.filter(product => product.category === category)
      }
    },
    selectProduct(productId) {
      this.$emit('select-product', productId)
    },
    addToCart(product) {
      this.$emit('add-to-cart', product)
    }
  }
}
</script>
