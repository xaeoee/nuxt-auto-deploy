<template>
  <div id="app" @mousemove="trackMouse">
    <header>
      <h1>Welcome to My Personal Development Blog</h1>
      <p>Follow along on my journey of growth and self-improvement.</p>
    </header>
    <div class="mouse-tracker" :style="trackerStyle"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mouseX: 0,
      mouseY: 0,
    };
  },
  computed: {
    trackerStyle() {
      return {
        left: `${this.mouseX}px`,
        top: `${this.mouseY}px`,
        transition: 'all 0.2s ease',
        position: 'absolute',
        pointerEvents: 'none',  // Prevents the tracker from interfering with clicks
        width: '20px',
        height: '20px',
        borderRadius: '50%',
        backgroundColor: 'rgba(255, 99, 71, 0.5)'
      };
    }
  },
  methods: {
    trackMouse(event) {
      this.mouseX = event.clientX;
      this.mouseY = event.clientY;
    }
  }
};
</script>

<style>
#app {
  text-align: center;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}

header h1 {
  margin: 0;
  font-size: 2em;
  color: #333;
}

header p {
  color: #666;
  font-size: 1.2em;
}
</style>
