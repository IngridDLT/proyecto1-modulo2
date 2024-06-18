<template>
  <div class="mb-4">
    <label for="category" class="block text-sm font-medium text-gray-700">Select Category</label>
    <select id="category" @change="handleCategoryChange" class="mt-1 block w-60 pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
      <option value="">All</option>
      <option v-for="category in categories" :key="category" :value="category">{{ category }}</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    categories: {
      type: Array,
      required: true,
    },
  },
  emits: ['category-selected'],
  setup(props, { emit }) {
    const handleCategoryChange = (event) => {
      emit('category-selected', event.target.value)
    }

    return {
      handleCategoryChange,
    }
  },
}
</script>

  