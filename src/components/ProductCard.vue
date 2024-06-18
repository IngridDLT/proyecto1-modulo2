<template>
  <div class="border p-4 rounded cursor-pointer hover:shadow-lg transition">
    <img :src="product.image" alt="product image" class="w-full h-48 object-cover mb-2">
    <h3 class="font-semibold">{{ product.title }}</h3>
    <p class="text-gray-500">{{ product.price }} USD</p>
    <button @click="handleAddToCart" class="mt-2 bg-blue-500 text-white px-4 py-2 rounded">Add to Cart</button>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  emits: ['click', 'add-to-cart'],
  setup(props, { emit }) {
    const handleAddToCart = (event) => {
      event.stopPropagation()
      emit('add-to-cart', props.product)
    }

    return {
      handleAddToCart,
    }
  },
}
</script>

  