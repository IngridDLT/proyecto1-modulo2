<template>
    <div class="mt-4 p-4 border rounded">
      <h2 class="text-xl font-semibold">{{ product.title }}</h2>
      <p class="text-gray-700">{{ product.description }}</p>
      <p class="text-gray-900 font-bold mt-2">{{ product.price }} USD</p>
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
  }
  </script>
  