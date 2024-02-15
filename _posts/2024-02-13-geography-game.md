<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Geography Trivia Game</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      background-color: #FAFAFA;
      margin: 0;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    h1 {
      color: #333;
    }
    #instructions, #score {
      text-align: center;
      margin: 10px 0;
    }
    .question-container {
      display: none;
      background-color: #FFFFFF;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 600px;
      margin: 20px 0;
    }
    .options li {
      margin: 10px 0;
      padding: 10px;
      background-color: #EEEEEE;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .options li:hover {
      background-color: #DDDDDD;
    }
    .show {
      display: block;
      animation: fadeIn 0.5s;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    #next-button {
      padding: 10px 20px;
      font-size: 16px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      display: none;
    }
    #next-button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>

  <h1>Geography Trivia</h1>

  <div id="instructions">
    <p>Put Your Geography Knowledge to The Test!</p>
  </div>

  <div id="questions-container"></div>

  <button id="next-button">Next Question</button>

  <div id="score">Your Score: <span id="current-score">0</span></div>

  <script>
    let currentQuestionIndex = 0;

    async function fetchTriviaQuestions() {
      const response = await fetch('https://opentdb.com/api.php?amount=10&category=22&difficulty=easy&type=multiple');
      const data = await response.json();
      const questions = data.results;
      populateQuestions(questions);
    }

    function populateQuestions(questions) {
      questions.forEach((question, index) => {
        const questionDiv = document.createElement('div');
        questionDiv.classList.add('question-container');
        questionDiv.innerHTML = `
          <h2>Question ${index + 1}</h2>
          <p class="question">${question.question}</p>
          <ul id="options${index}" class="options"></ul>
          <p class="answer" id="answer${index}"></p>
        `;
        document.getElementById('questions-container').appendChild(questionDiv);

        const options = [...question.incorrect_answers, question.correct_answer];
        options.sort(() => Math.random() - 0.5);

        options.forEach(option => {
          const li = document.createElement('li');
          li.textContent = option;
          li.addEventListener('click', () => checkAnswer(option, question.correct_answer, index, questions.length));
          document.getElementById(`options${index}`).appendChild(li);
        });
      });

      displayQuestion(currentQuestionIndex);
    }

    function displayQuestion(index) {
      const questions = document.querySelectorAll('.question-container');
      if (questions[index]) {
        questions.forEach(q => q.classList.remove('show'));
        questions[index].classList.add('show');
        document.getElementById('next-button').style.display = 'none';
      }
    }

    function checkAnswer(selected, correct, index, totalQuestions) {
      const answerElement = document.getElementById(`answer${index}`);
      if (selected === correct) {
        answerElement.textContent = 'Correct! 🎉';
        updateScore(1);
      } else {
        answerElement.textContent = 'Incorrect. 😔';
      }
      document.querySelectorAll('.question-container')[index].querySelectorAll('li').forEach(li => li.style.pointerEvents = 'none');
      if (index + 1 < totalQuestions) {
        document.getElementById('next-button').style.display = 'inline-block';
      }
    }

    document.getElementById('next-button').addEventListener('click', () => {
      if (currentQuestionIndex + 1 < document.querySelectorAll('.question-container').length) {
        currentQuestionIndex++;
        displayQuestion(currentQuestionIndex);
      }
    });

    function updateScore(points) {
      const scoreElement = document.getElementById('current-score');
      scoreElement.textContent = parseInt(scoreElement.textContent) + points;
    }

    fetchTriviaQuestions();
  </script>
</body>
</html>
