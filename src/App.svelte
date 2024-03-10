<script lang="ts">
  import Canvas from './components/Canvas.svelte';
  import Explanation from './components/Explanation.svelte';
  const width = 1000;
  const radius = width / 2;

  let points: [number, number, boolean][] = [];

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

    points = [...points, [x, y, inCircle]];

    if (inCircle) circlePoints++;
    totalPoints++;
  };

  $: ratio = totalPoints ? circlePoints / totalPoints : 0;
  $: estimate = ratio * 4;
</script>

<main>
  <Canvas {radius} {points} />

  <div class="stats">
    <ul>
      <li><b>Points inside Circle: {circlePoints}</b></li>
      <li><b>Total Points: {totalPoints}</b></li>
      <li><b>Ratio: {ratio}</b></li>
      <li><b>Pi Estimate: {estimate}</b></li>
    </ul>
  </div>

  <div class="controls">
    <button on:click={addPoint}>Add Point</button>
    <Explanation />
  </div>
</main>

<style>
</style>
