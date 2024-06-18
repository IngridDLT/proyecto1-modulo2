<template>
  <div class="fixed top-4 right-4 p-4 border rounded shadow-lg bg-white z-50 w-64">
    <div class="flex items-center justify-between mb-4">
      <h2 class="text-xl font-semibold">Shopping Cart</h2>
      <button @click="closeCart" class="text-gray-500 hover:text-gray-700 focus:outline-none">
        <i class="fa-solid fa-times text-xl"></i>
      </button>
    </div>
    <div v-if="cartItems.length">
      <ul>
        <li v-for="item in cartItems" :key="item.id" class="mb-2">
          <div class="flex justify-between items-center">
            <span>{{ item.title }} - {{ item.price }} USD</span>
            <button @click="removeFromCart(item.id)" class="bg-red-500 text-white px-4 py-2 rounded">Remove</button>
          </div>
        </li>
      </ul>
    </div>
    <p v-else class="text-gray-500">Your cart is empty.</p>
  </div>
</template>

<script>
export default {
  props: {
    cartItems: {
      type: Array,
      required: true,
    },
  },
  emits: ['remove-from-cart', 'close'],
  setup(props, { emit }) {
    const removeFromCart = (productId) => {
      emit('remove-from-cart', productId)
    }

    const closeCart = () => {
      emit('close')
    }

    return {
      removeFromCart,
      closeCart,
    }
  },
}
</script>
