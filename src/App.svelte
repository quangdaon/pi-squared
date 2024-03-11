<script lang="ts">
  import Canvas from './components/Canvas.svelte';
  import Explanation from './components/Explanation.svelte';
  const width = 1000;
  const radius = width / 2;
  let canvas: Canvas;
  let hideCanvas = false;

  let autoplay = false;
  let autoplayRateSelection = 0;

  let circlePoints = 0;
  let totalPoints = 0;

  const isInCircle = (x: number, y: number) => {
    const adjustedX = Math.abs(x - radius);
    const adjustedY = Math.abs(y - radius);

    const slope = Math.sqrt(adjustedX ** 2 + adjustedY ** 2);

    return slope <= radius;
  };

  const addPoint = () => {
    const x = Math.floor(Math.random() * width);
    const y = Math.floor(Math.random() * width);

    const inCircle = isInCircle(x, y);

    canvas.addPoint(x, y, inCircle);

    if (inCircle) circlePoints++;
    totalPoints++;
  };

  requestAnimationFrame(function loop() {
    if (autoplay) {
      for (let i = 0; i < autoplayRate; i++) {
        addPoint();
      }
    }

    requestAnimationFrame(loop);
  });

  $: ratio = totalPoints ? circlePoints / totalPoints : 0;
  $: estimate = ratio * 4;
  $: autoplayRate = 10 ** autoplayRateSelection;
</script>

<main>
  <Canvas {radius} hidden={hideCanvas} bind:this={canvas} />

  <div class="stats">
    <ul>
      <li><b>Points inside Circle:</b> {circlePoints.toLocaleString()}</li>
      <li><b>Total Points:</b> {totalPoints.toLocaleString()}</li>
      <li><b>Ratio:</b> {ratio}</li>
      <li><b>Pi Estimate:</b> {estimate}</li>
    </ul>
  </div>

  <div class="controls">
    <div>
      <label>
        <input type="checkbox" bind:checked={hideCanvas} /> Hide Visual
      </label>
    </div>
    <div>
      <label>
        <input type="checkbox" bind:checked={autoplay} /> Autoplay
      </label>
    </div>
    {#if autoplay}
      <div>
        <label for="autoplaySpeed">Autoplay Speed</label>
        <input
          type="range"
          min="0"
          max="4"
          bind:value={autoplayRateSelection}
        />
        {autoplayRate.toLocaleString()}
      </div>
    {:else}
      <button on:click={addPoint}>Add Point</button>
    {/if}
    <Explanation />
  </div>
</main>

<style>
</style>
