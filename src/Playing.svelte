<script>
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";
  import { fly, fade } from "svelte/transition";

  const progress = tweened(0.3, {
    duration: 400,
    easing: cubicOut
  });
  export let time;
  export let askQuestion;
  export let checkAnswer;
  export let isAnswerCorrect;
  export let visible;
  export let visibleAnswer;
</script>

<style>
  progress {
    margin: 2rem 1rem 1rem 1rem;
    width: 80%;
    background-color: #89cdfa;
    height: 1rem;
    border: none;
    border-radius: 10px;
    box-shadow: -1px 2px 5px rgba(1, 26, 42, 0.5);
  }
  .question__container {
    max-width: 80%;
    font-size: 1rem;
    flex: 1;
  }

  .question__speech-bubble {
    margin-top: 0;
    margin-bottom: 1rem;
    position: relative;
    background: #00aabb;
    border-radius: 0.08em;
    color: white;
    padding: 1rem;
  }

  .question__speech-bubble:after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 10%;
    width: 0;
    height: 0;
    border: 20px solid transparent;
    border-top-color: #00aabb;
    border-bottom: 0;
    border-right: 0;
    margin-left: -10px;
    margin-bottom: -20px;
  }
  ul {
    margin-left: 0.2rem;
    margin-bottom: 0;
    background: rgba(206, 231, 248, 0.5);
    padding: 1rem;
  }
  li {
    cursor: pointer;
    padding-bottom: 0.5rem;
    list-style: none;
    color: #053e64;
    font-size: 5vw;
  }
  li:last-child {
    padding-bottom: 0;
  }
  span {
    font-weight: bold;
  }
  .question__feedback {
    font-size: 1.5rem;
    font-family: "Sucrose Bold Two";
    text-align: center;
    font-variant: petite-caps;
    margin: 0;
  }

  .good {
    color: #0099ff;
  }
  .bad {
    color: #a50000;
  }

  .answer__feedback {
    background: #55b4f3;
    color: white;
    padding: 1rem;
    font-variant: petite-caps;
    text-align: center;
    border-bottom-right-radius: 10px;
  }

  @media (min-width: 700px) {
    .question__speech-bubble,
    .answer__feedback,
    .good,
    .bad,
    li {
      font-size: 2vw;
    }
  }
</style>

<progress value={(time * 3) / 100} />

{#if visible}
  <div class="question__container" transition:fly={{ y: 300, duration: 800 }}>
    {#if askQuestion}
      <p class="question__speech-bubble">
        {@html askQuestion.question}
      </p>
      <ul>
        {#each askQuestion.incorrect_answers as q}
          <li {q} on:click={checkAnswer}>
            <span>? -</span>
            {@html q}
          </li>
        {/each}
      </ul>
      {#if isAnswerCorrect === 'yes'}
        <p class="question__feedback good">correct</p>
        {#if visibleAnswer}
          <p in:fade class="answer__feedback">
            {@html askQuestion.correct_answer}
          </p>
        {/if}
      {:else if isAnswerCorrect === 'no'}
        <p class="question__feedback bad">incorrect</p>
        {#if visibleAnswer}
          <p in:fade class="answer__feedback">
            {@html askQuestion.correct_answer}
          </p>
        {/if}
      {/if}
    {:else}
      <p>Loading...</p>
    {/if}
  </div>
{/if}
