<template>
  <div class="filter-bar">
    <input
      type="text"
      class="search-input"
      placeholder="Search by title or location..."
      :value="searchTerm"
      @input="$emit('update:searchTerm', $event.target.value)"
    />

    <button class="sort-button" @click="$emit('toggle-sort')">
      Sort by price: {{ sortOrder === 'asc' ? 'Low to High ↑' : 'High to Low ↓' }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'FilterBar',
  props: {
    searchTerm: {
      type: String,
      default: ''
    },
    sortOrder: {
      type: String,
      default: 'asc'
    }
  },
  emits: ['update:searchTerm', 'toggle-sort']
}
</script>
