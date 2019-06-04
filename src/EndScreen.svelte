<script>
  export let good;
  export let bad;
  export let restart;
</script>

<style>
  section {
    flex: 1;
  }
</style>

<section>
  <p>Correct answers: {good}</p>
  <p>Wrong answers: {bad}</p>
  <button on:click={restart}>Play Again</button>
</section>
