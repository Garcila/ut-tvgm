<script>
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";
  import { fly } from "svelte/transition";

  const progress = tweened(0.3, {
    duration: 400,
    easing: cubicOut
  });
  export let time;
  export let askQuestion;
  export let checkAnswer;
  export let isAnswerCorrect;
  export let visible;
</script>

<style>
  progress {
    display: block;
    width: 100%;
  }
  button {
    display: block;
  }
</style>

<progress value={(time * 3) / 100} />

{#if visible}
  <div transition:fly={{ y: 300, duration: 800 }}>
    {#if askQuestion}
      <h3>
        {@html askQuestion.question}
      </h3>
      <ul>
        {#each askQuestion.incorrect_answers as q}
          <button {q} on:click={checkAnswer}>
            {@html q}
          </button>
        {/each}
      </ul>
      {#if isAnswerCorrect === 'yes'}
        <p>Correct!</p>
      {:else if isAnswerCorrect === 'no'}
        <p>Incorrect!</p>
        <h2>
          The correct answer is
          {@html askQuestion.correct_answer}
        </h2>
      {/if}
    {:else}
      <p>Loading...</p>
    {/if}
  </div>
{/if}
