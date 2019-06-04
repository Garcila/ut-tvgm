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
    flex: 1;
  }
</style>

<section>
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
