<template>
  <div id="app" @mousemove="handleMouseMove">
    <h1>Welcome to My Blog</h1>
    <p>Explore my journey and insights.</p>
    <div class="circle" :style="circleStyle"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mouseX: 0,
      mouseY: 0,
      requestId: null
    };
  },
  computed: {
    circleStyle() {
      return {
        position: 'absolute',
        width: '50px',
        height: '50px',
        borderRadius: '50%',
        backgroundColor: 'red',
        transform: `translate(${this.mouseX - 25}px, ${this.mouseY - 25}px)`,
        willChange: 'transform'
      };
    }
  },
  methods: {
    updatePosition() {
      this.requestId = requestAnimationFrame(this.updatePosition);
      // update your circle's position here if you have more complex animations
    },
    handleMouseMove(event) {
      this.mouseX = event.clientX;
      this.mouseY = event.clientY;
      if (!this.requestId) {
        this.updatePosition();
      }
    }
  },
  mounted() {
    this.updatePosition();
  },
  beforeDestroy() {
    if (this.requestId) {
      cancelAnimationFrame(this.requestId);
    }
  }
};
</script>

<style>
#app {
  position: relative;
  height: 100vh;
  text-align: center;
}

h1, p {
  position: relative;
  z-index: 1;
}
</style>
