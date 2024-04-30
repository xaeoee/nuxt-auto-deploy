<template>
  <div id="app" @mousemove="trackMouse" @click="popEffect">
    <header>
      <h1>Welcome to My Personal Development Blog</h1>
      <p>Follow along on my journey of growth and self-improvement.</p>
    </header>
    <div class="mouse-tracker" v-for="delay in [0, 100, 200, 300]" :key="delay" :style="trackerStyle(delay)"></div>
    <transition-group name="pop" tag="div">
      <div v-for="item in pops" :key="item.key" class="pop" :style="item.style"></div>
    </transition-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mouseX: 0,
      mouseY: 0,
      pops: [],
      nextPopKey: 0
    };
  },
  computed: {
    trackerStyle() {
      return delay => ({
        left: `${this.mouseX}px`,
        top: `${this.mouseY}px`,
        transition: `all ${0.2 + delay / 1000}s ease`,
        position: 'absolute',
        pointerEvents: 'none',
        width: '20px',
        height: '20px',
        borderRadius: '50%',
        backgroundColor: `rgba(255, 99, 71, ${1 - delay / 1000})`
      });
    }
  },
  methods: {
    trackMouse(event) {
      this.mouseX = event.clientX;
      this.mouseY = event.clientY;
    },
    popEffect(event) {
      const popStyle = {
        left: `${event.clientX - 10}px`,
        top: `${event.clientY - 10}px`,
        position: 'absolute',
        width: '20px',
        height: '20px',
        borderRadius: '50%',
        backgroundColor: 'rgba(100, 149, 237, 0.5)',
        animation: 'pop-animation 0.5s forwards'
      };
      this.pops.push({ key: this.nextPopKey++, style: popStyle });
      setTimeout(() => {
        this.pops.shift();
      }, 500);  // Remove pop after animation completes
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

.pop {
  pointer-events: none;
}

@keyframes pop-animation {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  100% {
    transform: scale(1.5);
    opacity: 0;
  }
}
</style>
