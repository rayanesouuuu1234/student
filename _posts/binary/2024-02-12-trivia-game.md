# Trivia Game

Welcome to the Trivia Game! Test your knowledge with these questions.

## Instructions

1. Answer each question to the best of your ability.
2. Each correct answer earns you a point.
3. Have fun!

---

## Questions

<!-- Questions will be dynamically populated from the API -->

<!-- API Endpoint: https://opentdb.com/api.php?amount=5&type=multiple -->

<!-- Placeholder for questions -->
<!-- Question 1 -->
<details>
  <summary>Question 1</summary>
  <p id="question1"></p>
  <details>
    <summary>Options</summary>
    <ul id="options1"></ul>
  </details>
  <p id="answer1"></p>
</details>

<!-- Question 2 -->
<details>
  <summary>Question 2</summary>
  <p id="question2"></p>
  <details>
    <summary>Options</summary>
    <ul id="options2"></ul>
  </details>
  <p id="answer2"></p>
</details>

<!-- Question 3 -->
<details>
  <summary>Question 3</summary>
  <p id="question3"></p>
  <details>
    <summary>Options</summary>
    <ul id="options3"></ul>
  </details>
  <p id="answer3"></p>
</details>

<!-- Question 4 -->
<details>
  <summary>Question 4</summary>
  <p id="question4"></p>
  <details>
    <summary>Options</summary>
    <ul id="options4"></ul>
  </details>
  <p id="answer4"></p>
</details>

<!-- Question 5 -->
<details>
  <summary>Question 5</summary>
  <p id="question5"></p>
  <details>
    <summary>Options</summary>
    <ul id="options5"></ul>
  </details>
  <p id="answer5"></p>
</details>

---

## Your Score: 0

<!-- JavaScript code to fetch and populate questions from the API -->
<script>
  async function fetchTriviaQuestions() {
    const response = await fetch('https://opentdb.com/api.php?amount=5&type=multiple');
    const data = await response.json();

    const questions = data.results;
    for (let i = 0; i < questions.length; i++) {
      const questionElement = document.getElementById(`question${i + 1}`);
      const optionsElement = document.getElementById(`options${i + 1}`);
      const answerElement = document.getElementById(`answer${i + 1}`);

      questionElement.textContent = questions[i].question;
      
      // Randomly shuffle answer options
      const options = [...questions[i].incorrect_answers, questions[i].correct_answer];
      options.sort(() => Math.random() - 0.5);

      options.forEach((option, index) => {
        const li = document.createElement('li');
        li.textContent = option;
        li.addEventListener('click', () => checkAnswer(option, questions[i].correct_answer, answerElement));
        optionsElement.appendChild(li);
      });
    }
  }

  function checkAnswer(selectedAnswer, correctAnswer, answerElement) {
    if (selectedAnswer === correctAnswer) {
      answerElement.textContent = 'Correct! 🎉';
      updateScore(1);
    } else {
      answerElement.textContent = 'Incorrect. 😔';
    }
  }

  function updateScore(points) {
    const scoreElement = document.getElementById('score');
    const currentScore = parseInt(scoreElement.textContent);
    scoreElement.textContent = currentScore + points;
  }

  // Fetch questions when the page loads
  fetchTriviaQuestions();
</script>
