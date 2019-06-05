<script>
  export let startPlaying;
  export let category;

  function selectTopic(e) {
    const topic = parseInt(e.target.value);
    startPlaying(topic);
  }
</script>

<style>
  section {
    margin: 1rem;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  p {
    margin-top: -10px;
    font-variant-caps: petite-caps;
    color: #0b314b;
  }
  button {
    border: 1px solid #a6d5f5;
    padding: 0.5rem 6rem 0.5 6rem;
    margin-bottom: -1px;
    background-color: transparent;
    font-family: "Sucrose Bold Two";
    font-size: 0.8rem;
    color: #053e64;
    cursor: pointer;
  }

  button:nth-child(odd) {
    border-top-right-radius: 50px;
    border-bottom-right-radius: 50px;
    margin-right: -2rem;
    border-left: none;
  }
  button:nth-child(even) {
    border-right: none;
    border-top-left-radius: 50px;
    border-bottom-left-radius: 50px;
    margin-left: -2rem;
  }
</style>

<section>
  <p>select a category to start</p>
  <button on:click={selectTopic} value="10">books</button>
  <button on:click={selectTopic} value="9">general</button>
  <button on:click={selectTopic} value="11">movies</button>
  <button on:click={selectTopic} value="15">games</button>
  <button on:click={selectTopic} value="17">science</button>
  <button on:click={selectTopic} value="18">computers</button>
  <button on:click={selectTopic} value="19">math</button>
  <button on:click={selectTopic} value="22">geography</button>
  <button on:click={selectTopic} value="23">history</button>
  <button on:click={selectTopic} value="25">art</button>
</section>
