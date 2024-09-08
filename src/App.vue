<template>
  <div v-if="isLoading" class="fixed inset-0 flex items-center justify-center backdrop-blur-md z-50">
    <loadingSpez @loadingComplete="onLoadingComplete" />
  </div>
  <div @mousemove="handleMouseMove" class="scale-100 md:scale-110">
    <router-view :style="parallaxStyle" />
  </div>
</template>

<script>
import loadingSpez from './components/loadingSpez.vue';

export default {
  components: {
    loadingSpez
  },
  data() {
    return {
      mouseX: 0,
      mouseY: 0,
      isLoading: true,
    }
  },
  computed: {
    parallaxStyle() {
      const movementX = (this.mouseX - window.innerWidth / 2) / 20;
      const movementY = (this.mouseY - window.innerHeight / 2) / 20;
      return {
        transform: `translate(${movementX}px, ${movementY}px)`
      };
    },
  },
  methods: {
    onLoadingComplete() {
      this.isLoading = false;
    },
    handleMouseMove(event) {
      this.mouseX = event.clientX;
      this.mouseY = event.clientY;
    }
  },
}
</script>