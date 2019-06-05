<script>
  export let good;
  export let bad;
  export let restart;
</script>

<style>
  section {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: "Sucrose Bold Two";
  }
  button {
    border-radius: 50%;
    height: 6rem;
    width: 6rem;
    border: none;
    background-color: #0b314b;
    color: white;
    transition: all 0.1s ease-in;
  }

  button:hover {
    color: #0b314b;
    background-color: #ffffff;
    border: 1px solid #0b314b;
    cursor: pointer;
  }
  button:active {
    color: #ffffff;
    background-color: #0a2d44;
    border: 1px solid #0b314b;
    cursor: pointer;
    transform: scale(0.95);
  }
</style>

<section>
  <p>Correct answers: {good}</p>
  <p>Wrong answers: {bad}</p>
  <button on:click={restart}>Play Again</button>
</section>
