<script lang="ts">
  import { onMount } from 'svelte';

  export let radius: number;
  export let hidden = false;

  let canvas: HTMLCanvasElement;
  const colorSquare = '#cbb9a8';
  const colorCircle = '#145c9e';

  onMount(() => {
    const ctx = canvas.getContext('2d');

    ctx.fillStyle = colorSquare;
    ctx.fillRect(0, 0, radius * 2, radius * 2);

    ctx.fillStyle = colorCircle;
    ctx.beginPath();
    ctx.arc(radius, radius, radius, 0, 2 * Math.PI);
    ctx.fill();
  });

  export const addPoint = (x: number, y: number, inCircle: boolean) => {
    const ctx = canvas.getContext('2d');

    ctx.fillStyle = inCircle ? colorSquare : colorCircle;
    ctx.beginPath();
    ctx.arc(x, y, 2, 0, 2 * Math.PI);
    ctx.fill();
  };
</script>

<canvas
  width={radius * 2}
  height={radius * 2}
  class="canvas"
  class:hidden
  bind:this={canvas}
/>

<style>
  .canvas {
    display: block;
    width: 100%;
  }

  .canvas.hidden {
    display: none;
  }

  @media only screen and (min-width: 600px) {
    .canvas {
      display: block;
      flex: 0 0 1;
      width: var(--canvas-width);
    }
  }
</style>
