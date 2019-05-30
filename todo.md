# Steps

[x] - Call API and store the 10 questions to ask (start just with books)
    - https://opentdb.com/api.php?amount=10&category=10&type=multiple

[] - Require user input to start the game

[] - New Page  

  [] - Present the User with a question and four choices

  [] - Present time left to answer the question

    [] - If an answer is selected or

    [] - If the time runs out

      [] - Show if the selection was correct or wrong

      [] - Show the correct answer

      [] - Have an image related to the answer (Maybe Giphy will be a good choice)

      [] - After a few seconds (aprx 5) move to the next question

      [] - Reset the timer and repeat the process until all the questions have been asked

[] - New Page Ending

  [] - Show a record of correct and incorrect answers, as well as unanswered questions

  [] - Have a button that resets the state of the game

## Time

Steps in handling time in the game

[] - Have a function that keeps track of time

[] - It starts running as soon as the user provides input to start the game

[] - SetTimeout of 30 seconds for each question

[] - SetTimeout of 5 seconds for each answer feedback

[] - Update the state of the game (question, list of answers and time remaining after each answer feedback)
