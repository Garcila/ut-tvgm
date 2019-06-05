<script>
  import { onMount } from "svelte";
  import Header from "./Header.svelte";
  import EndScreen from "./EndScreen.svelte";
  import StartScreen from "./StartScreen.svelte";
  import Playing from "./Playing.svelte";
  import Footer from "./Footer.svelte";

  let time = 30;
  let questions = [];
  let count = 0;
  let askQuestion;
  let isAnswerCorrect;
  let firstChoice = true;
  let playing = false;
  let end = false;
  let good = 0;
  let bad = 0;
  let category = 10;
  let interval = 0;

  let visibleAnswer = false;
  let visible = true;

  $: askQuestion = questions[count];
  $: time;

  async function getQuestions(category) {
    const URL = `https://opentdb.com/api.php?amount=10&category=${category}&type=multiple`;
    const res = await fetch(URL);
    const data = await res.json();
    questions = data.results;
    // Insert in a random position the correct answer in the incorrect answers array
    questions.forEach(q => {
      const randomPositionInArray = Math.floor(Math.random() * 4);
      q.incorrect_answers.splice(randomPositionInArray, 0, q.correct_answer);
    });
  }

  function startPlaying(category) {
    getQuestions(category);
    playing = true;
    interval = setInterval(() => {
      if (time > 0 && !end) {
        time = time - 1;
        console.log(time);
      } else {
        time = 30;
        visible = true;
        handleCount();
      }
    }, 1000);
    end && clearInterval(interval);
  }

  function handleCount() {
    count < questions.length - 1 ? (count += 1) : (end = true);
    isAnswerCorrect = "";
    firstChoice = true;
  }

  function checkAnswer(e) {
    if (firstChoice) {
      const answered = e.target.attributes.q.value;
      if (answered === askQuestion.correct_answer) {
        isAnswerCorrect = "yes";
        visibleAnswer = true;
        good++;
      } else {
        isAnswerCorrect = "no";
        visibleAnswer = true;
        bad++;
      }
      // Decrease available time to 3 seconds once the question has been answered
      setTimeout(() => {
        (time = 0), (visible = false);
      }, 3000);
    }
    firstChoice = false;
  }

  function restart() {
    count = 0;
    questions = [];
    isAnswerCorrect = "";
    firstChoice = true;
    playing = false;
    end = false;
    clearInterval(interval);
    getQuestions();
  }
</script>

<style>

</style>

<Header />
{#if !playing && !end}
  <StartScreen {startPlaying} {category} />
{:else if playing && !end}
  <Playing
    {time}
    {askQuestion}
    {checkAnswer}
    {isAnswerCorrect}
    {visible}
    {visibleAnswer} />
{:else}
  <EndScreen {good} {bad} {restart} />
{/if}
<Footer />
