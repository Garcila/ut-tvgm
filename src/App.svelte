<script>
  import { onMount } from "svelte";
  import Header from "./Header.svelte";
  import EndScreen from "./EndScreen.svelte";
  import StartScreen from "./StartScreen.svelte";
  import Playing from "./Playing.svelte";

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

  let visible = true;

  $: askQuestion = questions[count];
  $: time;

  onMount(() => {
    getQuestions();
  });

  async function getQuestions() {
    const URL = `https://opentdb.com/api.php?amount=2&category=10&type=multiple`;
    const res = await fetch(URL);
    const data = await res.json();
    questions = data.results;
    // Insert in a random position the correct answer in the incorrect answers array
    questions.forEach(q => {
      const randomPositionInArray = Math.floor(Math.random() * 4);
      q.incorrect_answers.splice(randomPositionInArray, 0, q.correct_answer);
    });
  }

  function startPlaying() {
    playing = true;
    const interval = setInterval(() => {
      if (time > 0 && !end) {
        time -= 1;
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
      // e.target.classList.add("active");
      const answered = e.target.attributes.q.value;
      if (answered === askQuestion.correct_answer) {
        isAnswerCorrect = "yes";
        good++;
      } else {
        isAnswerCorrect = "no";
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
    end = false;
    time = 30;
    count = 0;
    questions = [];
    askQuestion;
    isAnswerCorrect = "";
    firstChoice = true;
    playing = true;
    end = false;
    good = 0;
    bad = 0;
    getQuestions();
  }
</script>

<style>
 
</style>

<Header />
{#if !playing && !end}
  <StartScreen {startPlaying} />
{:else if playing && !end}
  <Playing {time} {askQuestion} {checkAnswer} {isAnswerCorrect} {visible} />
{:else}
  <EndScreen {good} {bad} {restart} />
{/if}
