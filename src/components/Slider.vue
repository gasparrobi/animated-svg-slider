<template>
  <div
    class="slider-wrapper"
    ref="sliderWrapper"
    @mousedown="onMouseDown"
    @mouseup="onMouseUp"
    @mouseleave="onMouseUp"
    @mousemove="onMouseMove"
  >
    <svg ref="svg" class="slider" width="300px" height="480px" viewBox="0 0 300 480">
      <defs>
        <symbol id="lines" shape-rendering="crispEdges">
          <path class="line-path" d="M 237 60 l 33 0"></path>
          <path class="line-path" d="M 248 90 l 22 0"></path>
          <path class="line-path" d="M 258 120 l 12 0"></path>
          <path class="line-path" d="M 258 150 l 12 0"></path>
          <path class="line-path" d="M 258 180 l 12 0"></path>
          <path class="line-path" d="M 258 210 l 12 0"></path>
          <path class="line-path" d="M 258 240 l 12 0"></path>
          <path class="line-path" d="M 258 270 l 12 0"></path>
          <path class="line-path" d="M 258 300 l 12 0"></path>
          <path class="line-path" d="M 258 330 l 12 0"></path>
          <path class="line-path" d="M 258 360 l 12 0"></path>
          <path class="line-path" d="M 248 390 l 22 0"></path>
          <path class="line-path" d="M 237 420 l 33 0"></path>
        </symbol>

        <clipPath id="slider-clip-path">
          <path class="slider-path" ref="target2" d="M 0 200 l 300 0 l 0 480 l -300 0 Z"></path>
        </clipPath>
      </defs>
      <use xlink:href="#lines" class="line-path--blue"></use>
      <path class="slider-path" ref="target" d="M 0 200 q 150 0 300 0 l 0 480 l -300 0 Z"></path>
      <use xlink:href="#lines" class="line-path--white" clip-path="url(#slider-clip-path)"></use>
    </svg>

    <div class="value" :style="valueStyle">{{ rangeValue }}</div>
    <div class="description" :style="descriptionStyle">
      <transition name="zoom" mode="out-in">
        <div :key="rangeDescription">{{ rangeDescription }}</div>
      </transition>
    </div>
  </div>
</template>

<script>
import anime from "animejs";

export default {
  name: "Slider",
  props: {
    msg: String
  },

  data() {
    return {
      buffer: 40,
      min: 80,
      max: 400,
      mouseY: 0,
      moveY: 0,
      currentY: 200,
      target: null,
      target2: null
    };
  },

  computed: {
    svgHeight() {
      if (this.moveY < this.buffer && this.moveY > -this.buffer)
        return this.currentY;
      const h =
        this.currentY +
        this.moveY +
        (this.moveY < 0 ? this.buffer : -this.buffer);
      if (h < this.min) return this.min;
      if (h > this.max) return this.max;
      return h;
    },

    bow() {
      const b = this.moveY;
      if (Math.abs(b) < this.buffer) return b;
      return b < 0 ? -this.buffer : this.buffer;
    },

    valueStyle() {
      return `
        top: ${this.svgHeight + 30}px;
        transform: scale(${1.7 - this.svgHeight / 480});
        transform-origin: 0% 0%;
      `;
    },

    descriptionStyle() {
      return `
        top: ${this.svgHeight - 45}px;
        transform-origin: left center;
      `;
    },

    rangeDescription() {
      if (480 - this.svgHeight > 320) return "godlike!";
      if (480 - this.svgHeight > 210) return "unstoppable!";
      if (480 - this.svgHeight > 120) return "way to go!";
      return "nice";
    },

    rangeValue() {
      return 480 - this.svgHeight;
    }
  },

  mounted() {
    this.target = this.$refs.target;
    this.target2 = this.$refs.target2;
    const slider = this.$refs.sliderWrapper;
    slider.addEventListener("touchstart", this.onMouseDown);
    slider.addEventListener("touchend", this.onMouseUp);
    slider.addEventListener("touchmove", this.onMouseMove);
  },

  beforeDestroy() {},

  methods: {
    onMouseDown(e) {
      e.preventDefault();
      anime.remove([this.target, this.target2]);
      this.mouseY = e.pageY;
    },

    onMouseUp(e) {
      e.preventDefault();

      anime({
        targets: [this.target, this.target2],
        d: `M 0 ${this.svgHeight} q 150 0 300 0 l 0 480 l -300 0 Z`,
        duration: 3000,
        easing: "easeOutElastic(1, .2)"
        // elasticity: 880
      });

      this.currentY = this.svgHeight;
      this.mouseY = 0;
      this.moveY = 0;
    },

    onMouseMove(e) {
      e.preventDefault();
      if (this.mouseY) {
        const posY = e.pageY;
        this.moveY = posY - this.mouseY;
        this.target.setAttribute(
          "d",
          `M 0 ${this.svgHeight} q 150 ${this.bow} 300 0 l 0 480 l -300 0 Z`
        );
        this.target2.setAttribute(
          "d",
          `M 0 ${this.svgHeight} q 150 ${this.bow} 320 0 l 0 480 l -300 0 Z`
        );
      }
    }
  }
};
</script>

<style scoped>
.slider-wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  /* background-color: #dde7f3; */
}

svg {
  border-radius: 10px;
  box-shadow: 4px 2px 16px rgba(136, 165, 191, 0.48), -4px -2px 16px #fff;
}

.slider-path {
  fill: rgba(57, 117, 167, 0.445);
}

.line-path {
  z-index: 11000;
  stroke-width: 1px;
}

.line-path--blue {
  stroke: rgba(57, 117, 167, 0.445);
}

.line-path--white {
  stroke: white;
}

.value {
  position: absolute;
  left: 30px;
  color: #fff;
  font-size: 36px;
  font-weight: 600;
}

.description {
  position: absolute;
  white-space: nowrap;
  top: 30px;
  left: 30px;
  color: rgba(57, 117, 167, 0.445);
  font-size: 16px;
  font-weight: 600;
  transform-origin: left center;
}

/* TRANSITION */

.zoom-enter-active,
.zoom-leave-active {
  transition: opacity 0.2s;
  transform-origin: left center;
}
.zoom-enter, .zoom-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: scale3d(0.6, 0.6, 0.6);
  transform-origin: left center;
}
</style>
