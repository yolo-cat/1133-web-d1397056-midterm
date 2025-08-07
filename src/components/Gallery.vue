<template>
  <ul class="gallery">
    <li
      v-for="image in filteredImages"
      :key="image.id"
      :data-category="image.category"
      @mouseenter="startTimer(image.id)"
      @mouseleave="stopTimer(image.id)"
    >
      <span class="hover-timer">{{ timers[image.id] || '0.0s' }}</span>
      <img :src="image.src" :alt="image.alt">
    </li>
  </ul>
</template>

<script>
export default {
  name: 'Gallery',
  props: {
    images: {
      type: Array,
      required: true
    },
    activeFilter: {
      type: String,
      default: 'all'
    }
  },
  data() {
    return {
      timers: {},
      rafIds: {},
      startTimes: {}
    }
  },
  computed: {
    filteredImages() {
      if (this.activeFilter === 'all') {
        return this.images;
      }
      return this.images.filter(image => image.category === this.activeFilter);
    }
  },
  methods: {
    startTimer(imageId) {
      this.startTimes[imageId] = performance.now();
      this.timers[imageId] = '0.0s';
      this.updateTimer(imageId);
    },
    stopTimer(imageId) {
      if (this.rafIds[imageId]) {
        cancelAnimationFrame(this.rafIds[imageId]);
        delete this.rafIds[imageId];
      }
    },
    updateTimer(imageId) {
      const elapsed = ((performance.now() - this.startTimes[imageId]) / 1000).toFixed(1);
      this.timers[imageId] = `${elapsed}s`;
      this.rafIds[imageId] = requestAnimationFrame(() => this.updateTimer(imageId));
    }
  },
  beforeUnmount() {
    // 清理所有計時器
    Object.values(this.rafIds).forEach(rafId => {
      cancelAnimationFrame(rafId);
    });
  }
}
</script>

<style scoped>
.gallery {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1.5rem;
  list-style: none;
  padding: 0 1rem;
  width: 100%;
  max-width: 1200px;
}

.gallery li {
  background: #fff;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
  flex: 0 0 calc(33.333% - 1rem);
  max-width: 350px;
  min-width: 280px;
}

.gallery li:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 25px rgba(0,0,0,0.25);
}

.gallery img {
  width: 100%;
  height: 220px;
  display: block;
  object-fit: cover;
  transition: none;
  border-radius: 20px;
  border: 6px solid #fff;
}

.gallery img:hover {
  box-shadow: none;
  transform: none;
}

.hover-timer {
  position: absolute;
  top: 12px;
  left: 12px;
  background: rgba(0,0,0,0.7);
  color: #fff;
  padding: 6px 12px;
  border-radius: 12px;
  font-size: 1.1rem;
  z-index: 2;
  pointer-events: none;
  font-family: monospace;
  display: none;
  font-weight: bold;
  backdrop-filter: blur(5px);
}

.gallery li:hover .hover-timer {
  display: block;
}

/* 響應式設計 - 大螢幕 */
@media (min-width: 1200px) {
  .gallery {
    gap: 2rem;
  }

  .gallery li {
    flex: 0 0 calc(25% - 1.5rem);
  }
}

/* 響應式設計 - 平板 */
@media (max-width: 1024px) {
  .gallery li {
    flex: 0 0 calc(50% - 0.75rem);
  }
}

@media (max-width: 768px) {
  .gallery {
    gap: 1rem;
    padding: 0 0.5rem;
  }

  .gallery li {
    flex: 0 0 calc(50% - 0.5rem);
    min-width: 200px;
  }

  .gallery img {
    height: 180px;
  }

  .hover-timer {
    font-size: 1rem;
    padding: 4px 8px;
  }
}

/* 響應式設計 - 手機 */
@media (max-width: 600px) {
  .gallery {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }

  .gallery li {
    flex: none;
    width: 100%;
    max-width: 400px;
  }

  .gallery img {
    height: 200px;
  }
}

@media (max-width: 480px) {
  .gallery {
    gap: 0.8rem;
  }

  .gallery img {
    height: 180px;
  }

  .hover-timer {
    font-size: 0.9rem;
    top: 8px;
    left: 8px;
  }
}
</style>
