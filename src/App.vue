<template>
  <div id="app">
    <div id="title-description">
      <h1 id="title">Image Attention Experiment</h1>
      <p id="description">Hover your mouse over the image you're interested in to start the timer.</p>
    </div>

    <FilterBar
      :active-filter="activeCategory"
      @filter-change="handleFilterChange"
    />

    <Gallery
      :images="images"
      :active-filter="activeCategory"
    />
  </div>
</template>

<script>
import FilterBar from './components/FilterBar.vue'
import Gallery from './components/Gallery.vue'
import nature1 from '@/assets/nature1.jpg'
import nature2 from '@/assets/nature2.jpg'
import nature3 from '@/assets/nature3.jpg'
import nature4 from '@/assets/nature4.jpg'
import nature5 from '@/assets/nature5.jpg'
import city1 from '@/assets/city1.jpg'
import city2 from '@/assets/city2.jpg'
import city3 from '@/assets/city3.jpg'

export default {
  name: 'App',
  components: {
    FilterBar,
    Gallery
  },
  data() {
    return {
      activeCategory: 'all',
      images: [
        { id: 1, src: nature1, alt: 'Nature 1', category: 'nature' },
        { id: 2, src: nature2, alt: 'Nature 2', category: 'nature' },
        { id: 3, src: nature3, alt: 'Nature 3', category: 'nature' },
        { id: 4, src: nature4, alt: 'Nature 4', category: 'nature' },
        { id: 5, src: nature5, alt: 'Nature 5', category: 'nature' },
        { id: 6, src: city1, alt: 'City 1', category: 'city' },
        { id: 7, src: city2, alt: 'City 2', category: 'city' },
        { id: 8, src: city3, alt: 'City 3', category: 'city' }
      ]
    }
  },
  methods: {
    handleFilterChange(filter) {
      this.activeCategory = filter;
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: linear-gradient(135deg, #d67575 0%, #c66a6a 100%);
  min-height: 100vh;
  font-family: 'Arial', sans-serif;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  padding: 2rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

#title-description {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-bottom: 3rem;
  text-align: center;
  width: 100%;
}

#title {
  color: #222;
  font-size: 2.5rem;
  font-weight: bold;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.03);
  margin-bottom: 1rem;
}

#description {
  color: #222;
  font-size: 1.1rem;
  max-width: 600px;
  line-height: 1.5;
  text-shadow: 1px 1px 2px rgba(0,0,0,0.01);
}

@media (max-width: 768px) {
  #app {
    padding: 1.5rem 0.5rem;
  }

  #title-description {
    margin-bottom: 2rem;
  }

  #title {
    font-size: 2rem;
    color: #222;
  }

  #description {
    font-size: 1rem;
    color: #222;
  }
}

@media (max-width: 600px) {
  #title-description {
    margin-bottom: 1.5rem;
  }

  #title {
    font-size: 1.8rem;
    color: #222;
  }
}
</style>
