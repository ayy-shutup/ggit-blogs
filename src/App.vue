<template>
  <div class="body">
    <div class="cursor">
      <div class="cursor__ball cursor__ball--big">
        <svg height="30" width="30">
          <circle cx="15" cy="15" r="12" stroke-width="0"></circle>
        </svg>
      </div>

      <div class="cursor__ball cursor__ball--small">
        <svg height="10" width="10">
          <circle cx="5" cy="5" r="4" stroke-width="0"></circle>
        </svg>
      </div>
    </div>

    <div class="left">
      <h1>Hello</h1>
      <p>Check out this link:</p>
      <a class="hoverable">Hover meh</a>
    </div>

    <div class="right">
      <h1>Hello</h1>
      <p>Check out this link:</p>
      <a class="hoverable">Hover meh</a>
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap';

export default {
  name: 'CursorComponent',
  mounted() {
    this.initCursor();
  },
  methods: {
    initCursor() {
      const bigBall = this.$el.querySelector('.cursor__ball--big');
      const smallBall = this.$el.querySelector('.cursor__ball--small');
      const hoverables = this.$el.querySelectorAll('.hoverable');

      document.body.addEventListener('mousemove', this.onMouseMove.bind(this, bigBall, smallBall));
      hoverables.forEach(hoverable => {
        hoverable.addEventListener('mouseenter', this.onMouseHover.bind(this, bigBall));
        hoverable.addEventListener('mouseleave', this.onMouseHoverOut.bind(this, bigBall));
      });
    },
    onMouseMove(bigBall, smallBall, e) {
      gsap.to(bigBall, {
        duration: 0.4,
        x: e.pageX - 15,
        y: e.pageY - 15
      });
      gsap.to(smallBall, {
        duration: 0.1,
        x: e.pageX - 5,
        y: e.pageY - 7
      });
    },
    onMouseHover(bigBall) {
      gsap.to(bigBall, {
        duration: 0.3,
        scale: 4
      });
    },
    onMouseHoverOut(bigBall) {
      gsap.to(bigBall, {
        duration: 0.3,
        scale: 1
      });
    }
  }
};
</script>

<style scoped>
.body {
  height: 100vh;
  background: #010101;
  cursor: none;
  margin: 0;
  display: flex;
  font-family: monospace;
}

h1, p, a {
  color: #fff;
}

a {
  border-bottom: 2px solid #fff;
  padding: 10px 0;
  margin-top: 25px;
}

.cursor {
  pointer-events: none;
}

.cursor__ball {
  position: fixed;
  top: 0;
  left: 0;
  mix-blend-mode: difference;
  z-index: 1000;
}

.cursor__ball circle {
  fill: #f1f0f0;
}

.left, .right {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.right {
  background: #fff;
}

.right a {
  border-bottom: 2px solid #000;
}

.right h1, .right p, .right a {
  color: #000;
}
</style>
