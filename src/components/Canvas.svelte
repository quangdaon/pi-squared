<script lang="ts">
  export let radius: number;
  export let hidden = false;
  let points: SVGGElement;

  // Not keeping point in memory for performance
  export const addPoint = (x: number, y: number, inCircle: boolean) => {
    const point = document.createElementNS(
      'http://www.w3.org/2000/svg',
      'circle'
    );

    point.setAttribute('cx', x.toString());
    point.setAttribute('cy', y.toString());
    point.setAttribute('r', '2');
    point.classList.add('point');

    points.appendChild(point);
  };
</script>

<svg class="canvas" class:hidden viewBox="0 0 {radius * 2} {radius * 2}">
  <rect class="square" x="0" y="0" width={radius * 2} height={radius * 2} />
  <circle class="circle" cx={radius} cy={radius} r={radius} />
  <g class="points" bind:this={points}></g>
</svg>

<style>
  .canvas {
    --color-square: #f00;
    --color-circle: #0ff;
    display: block;
    width: 400px;
  }

  .canvas.hidden {
    display: none;
  }

  .square {
    fill: var(--color-square);
  }

  .circle {
    fill: var(--color-circle);
  }

  :global(.point) {
    fill: rgba(0, 0, 0, 0.5);
  }
</style>
