<script lang="ts">
  export let radius: number;
  export let points: [number, number, boolean][] = [];
</script>

<svg class="canvas" viewBox="0 0 {radius * 2} {radius * 2}">
  <rect class="square" x="0" y="0" width={radius * 2} height={radius * 2} />
  <circle class="circle" cx={radius} cy={radius} r={radius} />
  <g class="points">
    {#each points as [cx, cy]}
      <circle class="point" {cx} {cy} r="6" />
    {/each}
  </g>
</svg>

<style>
  .canvas {
    --color-square: #f00;
    --color-circle: #0ff;
    display: block;
    width: 400px;
  }

  .square {
    fill: var(--color-square);
  }

  .circle {
    fill: var(--color-circle);
  }

  .point {
    fill: black;
  }
</style>
