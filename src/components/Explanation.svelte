<script lang="ts">
  let dialog: HTMLDialogElement;
</script>

<button on:click={() => dialog.showModal()}>Explain</button>

<dialog bind:this={dialog}>
  <p>
    The formula to calculate the area of a circle is πr<sup>2</sup>. A square
    that perfect encloses a circle of radius r has an edge length of 2r, or an
    area of (2r)<sup>2</sup>. This can be rewritten as 4r<sup>2</sup>. This
    means that the ratio between the area of a circle and the area of its
    enclosing square is approximately π/4.
  </p>

  <p>
    We can use this knowledge to derive the value of π. Of course, to do so
    algorithmically, we need to already know the value of π to calculate the
    area of the circle. Another approach we can take is by using probability. If
    you split a square vertically down the middle and pick a random point within
    it, there is logically a 1/2 chance that the point resides in the left half
    of square. This is because each half has 1/2 the area of the full square.
    Similarly, the chance that a point chosen at random inside of a square also
    resides inside of an inscribed circle is π/4.
  </p>

  <p>
    If we select random points inside a square (y) and count the number that
    lands inside the circle (x), the proportion of x/y will converge to π/4.
    Therefore, we can estimate the value of π to be (x/y)*4.
  </p>

  <form method="dialog">
    <button>Cool!</button>
  </form>
</dialog>


<style>
  dialog {
    max-width: 42vw;
  }
</style>