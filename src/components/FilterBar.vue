<template>
  <nav class="filter-bar">
    <button
      v-for="filter in filters"
      :key="filter.value"
      :class="{ active: activeFilter === filter.value }"
      @click="$emit('filter-change', filter.value)"
    >
      {{ filter.label }}
    </button>
  </nav>
</template>

<script>
export default {
  name: 'FilterBar',
  props: {
    activeFilter: {
      type: String,
      default: 'all'
    }
  },
  emits: ['filter-change'],
  data() {
    return {
      filters: [
        { value: 'all', label: 'ALL' },
        { value: 'nature', label: 'Nature Landscapes' },
        { value: 'city', label: 'City Landscapes' }
      ]
    }
  }
}
</script>

<style scoped>
.filter-bar {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin: 2rem 0 3rem 0;
  flex-wrap: wrap;
}

.filter-bar button {
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  background: #e0e0e0;
  color: #222;
  font-size: 1rem;
  font-weight: 500;
  box-shadow: none;
  text-shadow: none;
  backdrop-filter: none;
}

.filter-bar button:hover {
  cursor: pointer;
  background: rgba(255,255,255,0.2);
  border-color: rgba(255,255,255,0.5);
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
}

.filter-bar button.active {
  background-color: #38b2ac;
  color: white;
  border-color: #38b2ac;
  box-shadow: 0 4px 15px rgba(56, 178, 172, 0.3);
}

.filter-bar button.active:hover {
  background-color: #2d9596;
  border-color: #2d9596;
}

@media (max-width: 768px) {
  .filter-bar {
    gap: 1rem;
    margin: 1.5rem 0 2.5rem 0;
  }

  .filter-bar button {
    padding: 0.7rem 1.2rem;
    font-size: 0.95rem;
  }
}

@media (max-width: 600px) {
  .filter-bar {
    gap: 0.8rem;
    margin: 1rem 0 2rem 0;
  }

  .filter-bar button {
    padding: 0.7rem 1rem;
    font-size: 0.9rem;
  }
}
</style>
