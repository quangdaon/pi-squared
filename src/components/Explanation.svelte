<script lang="ts">
  let dialog: HTMLDialogElement;
</script>

<button on:click={() => dialog.showModal()}>Explain</button>

<dialog bind:this={dialog}>
  <p>
    The formula to calculate the area of a circle is πr<sup>2</sup>. A square
    that perfectly encloses a circle of radius r has an edge length of 2r, or an
    area of (2r)<sup>2</sup>. This can be rewritten as 4r<sup>2</sup>. This
    means that the ratio between the area of a circle and the area of its
    enclosing square is πr<sup>2</sup>/4r<sup>2</sup>, which can be simplified
    to π/4.
  </p>

  <p>
    We can use this knowledge to derive the value of π. Of course, to do so
    algorithmically, we need to already know the value of π to calculate the
    area of the circle. Another approach we can take is by using probability. If
    one shape resides inside the perimeter of another shape and a point is
    randomly selected inside the outer shape, the probability that that point
    also overlaps with the inner shape is equal to the ratio in area between the
    two shapes. For example, if you split a square vertically down the middle
    and pick a random point within it, there is a 1/2 chance that the point
    resides in the left half of square.
  </p>

  <p>
    Similarly, the chance that a point chosen at random inside of a square also
    resides inside of an inscribed circle is π/4. If we select random points
    inside a square (y) and count the number that lands inside the circle (x),
    the proportion of x/y will converge to π/4. Therefore, we can estimate the
    value of π to be (x/y)*4.
  </p>

  <p>Check out <a href="https://www.quangdao.com/blog/pi-day-2024">my blog post</a> for more information.</p>

  <form method="dialog">
    <button>Cool!</button>
  </form>
</dialog>

<style>
  dialog {
    color: var(--color-foreground);
    background-color: var(--color-background);
    border-color: #cbb9a8;
  }

  dialog p {
    margin-top: 0;
  }

  @media only screen and (min-width: 600px) {
    dialog {
      max-width: 42vw;
    }
  }
</style>
