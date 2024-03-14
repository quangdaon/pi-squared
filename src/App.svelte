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

  <div class="info">
    <div class="stats">
      <ul>
        <li><b>Points inside Circle:</b> {circlePoints.toLocaleString()}</li>
        <li><b>Total Points:</b> {totalPoints.toLocaleString()}</li>
        <li><b>Ratio:</b> {ratio.toFixed(8)}</li>
        <li><b>Pi Estimate:</b> {estimate.toFixed(8)}</li>
      </ul>
    </div>

    <div class="controls">
      <div class="control">
        <label>
          <input type="checkbox" bind:checked={hideCanvas} /> Hide Visual
        </label>
      </div>
      <div class="control">
        <label>
          <input type="checkbox" bind:checked={autoplay} /> Autoplay
        </label>
      </div>
      <div class="control">
        <label for="autoplaySpeed">Autoplay Speed</label>
        <input
          type="range"
          min="0"
          max="4"
          bind:value={autoplayRateSelection}
        />
        {autoplayRate.toLocaleString()}
      </div>
    </div>

    <div class="actions">
      <button disabled={autoplay} on:click={addPoint}>Add Point</button>
      <Explanation />
    </div>
  </div>
</main>

<style>
  main {
    align-items: center;
  }

  .info {
    flex: 1 0 1;
    padding: 1em;
  }

  .stats ul {
    max-width: 100%;
    padding-left: 0;
    margin-left: 0;
    list-style-position: inside;
  }

  .stats ul li {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .actions {
    margin-top: 1em;
  }

  @media only screen and (min-width: 600px) {
    main {
      --canvas-width: 40vw;
      width: 100%;
      height: 100%;
      margin: auto;
      display: flex;
      align-items: center;
      gap: 2em;
      padding: 0 calc((100vh - var(--canvas-width)) / 2);
    }
  }
</style>
