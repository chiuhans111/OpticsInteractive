<template>
  <div id="app">
    <canvas width="500" height="500" ref="canvas"> </canvas>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      /**@type {HTMLCanvasElement} */
      canvas: null,
      /**@type {CanvasRenderingContext2D} */
      ctx: null,
      alive: false,

      // animations
      frames: 0,
      frames_per_cycle: 60,

      // properties
      props: {
        thickness: 50,
        incident_angle: 0
      },
    };
  },
  mounted() {
    this.canvas = this.$refs["canvas"];
    this.ctx = this.canvas.getContext("2d");
    this.alive = true;
    this.update();
  },
  destroyed() {
    this.alive = false;
  },
  methods: {
    update() {
      if (!this.alive) return;
      requestAnimationFrame(this.update);
      // frames
      this.frames++;
      this.frames = this.frames % this.frames_per_cycle;
      // let fac = this.frames / this.frames_per_cycle;

      // main
      let width = this.canvas.width;
      let height = this.canvas.height;
      let ctx = this.ctx;
      ctx.clearRect(0, 0, width, height);

      // ground
      let thickness = this.props.thickness;
      ctx.moveTo(0, height / 2 - thickness / 2);
      ctx.lineTo(width, height / 2 - thickness / 2);

      ctx.moveTo(0, height / 2 + thickness / 2);
      ctx.lineTo(width, height / 2 + thickness / 2);
      ctx.stroke();


      // incident wave

      


    },
  },
};
</script>

<style>
#app {
  margin: auto;
  max-width: 1000px;
  text-align: center;
}
</style>
