<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Geography Trivia Game</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f0f0f0;
      margin: 20px;
    }
    h1 {
      text-align: center;
      color: #333;
    }
    #instructions {
      margin-bottom: 20px;
      text-align: center;
    }
    details {
      background-color: #fff;
      border: 1px solid #ddd;
      margin-bottom: 10px;
      padding: 10px;
      border-radius: 5px;
    }
    summary {
      font-weight: bold;
      cursor: pointer;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      margin: 5px 0;
      padding: 8px;
      background-color: #eee;
      border-radius: 3px;
      cursor: pointer;
    }
    p {
      margin: 10px 0;
    }
    #score {
      text-align: center;
      font-size: 18px;
      font-weight: bold;
      color: #333;
    }
  </style>
</head>
<body>

  <h1>Geography Trivia</h1>

  <div id="instructions">
    <p>Welcome to the geography Game! Test your knowledge with these questions.</p>
    <p>Answer each question to the best of your ability. Each correct answer earns you a point. Have fun!</p>
  </div>

  <div id="questions-container">
    <!-- Questions will be dynamically populated from the API -->
  </div>

  <div id="score">Your Score: <span id="current-score">0</span></div>

  <!-- JavaScript code to fetch and populate questions from the API -->
  <script>
    async function fetchTriviaQuestions() {
      const response = await fetch('https://opentdb.com/api.php?amount=10&category=22&difficulty=easy&type=multiple');
      const data = await response.json();

      const questionsContainer = document.getElementById('questions-container');
      const questions = data.results;

      questions.forEach((question, index) => {
        const questionDiv = document.createElement('div');
        questionDiv.classList.add('question-container');
        questionDiv.innerHTML = `
          <details>
            <summary>Question ${index + 1}</summary>
            <p class="question" id="question${index + 1}">${question.question}</p>
            <ul id="options${index + 1}" class="options"></ul>
            <p class="answer" id="answer${index + 1}"></p>
          </details>
        `;

        questionsContainer.appendChild(questionDiv);

        const optionsElement = document.getElementById(`options${index + 1}`);

        // Randomly shuffle answer options
        const options = [...question.incorrect_answers, question.correct_answer];
        options.sort(() => Math.random() - 0.5);

        options.forEach((option, optionIndex) => {
          const li = document.createElement('li');
          li.textContent = option;
          li.addEventListener('click', () => checkAnswer(option, question.correct_answer, document.getElementById(`answer${index + 1}`)));
          optionsElement.appendChild(li);
        });
      });
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
      const scoreElement = document.getElementById('current-score');
      const currentScore = parseInt(scoreElement.textContent);
      scoreElement.textContent = currentScore + points;
    }

    // Fetch questions when the page loads
    fetchTriviaQuestions();
  </script>
</body>
</html>
