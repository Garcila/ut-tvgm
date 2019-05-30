<script>
  export let good;
  export let bad;
  export let restart;
</script>

<p>Correct answers: {good}</p>
<p>Wrong answers: {bad}</p>
<button on:click={restart}>Play Again</button>
