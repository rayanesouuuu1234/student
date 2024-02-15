<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Travel Recommendation Quiz</title>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet">
<style>
  body {
    font-family: 'Roboto', sans-serif;
    margin: 0;
    padding: 20px;
    background-color: #FAFAFA;
  }
  h1, p {
    text-align: center;
  }
  .question {
    display: none;
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    margin-bottom: 20px;
  }
  .show {
    display: block;
    animation: fadeIn 0.5s;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    margin: 10px 0;
    padding: 10px;
    background-color: #EEEEEE;
    border-radius: 5px;
    cursor: pointer;
  }
  li:hover {
    background-color: #DDDDDD;
  }
  button {
    display: block;
    width: 100%;
    padding: 10px;
    margin-top: 20px;
    font-size: 16px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  button:hover {
    background-color: #45a049;
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
</style>
</head>
<body>

<h1>Welcome to the Travel Recommendation Quiz!</h1>
<p>Answer the following questions to find out where you should travel.</p>

<div id="quiz"></div>

<script>
const questions = [
  {
    text: "What type of climate do you prefer?",
    options: ["Sunny and Mediterranean", "Cool and Nordic", "Warm and Tropical", "Crisp and Alpine"],
    values: ["Italy", "Iceland", "Thailand", "Switzerland"]
  },
  {
    text: "What activity sounds most appealing to you?",
    options: ["Exploring ancient ruins", "Chasing Northern Lights", "Relaxing on beautiful beaches", "Skiing in the mountains"],
    values: ["Italy", "Iceland", "Thailand", "Switzerland"]
  },
  {
    text: "What type of cuisine are you most interested in trying?",
    options: ["Pasta, Pizza, Gelato", "Fresh seafood", "Spicy Thai dishes", "Swiss chocolate and cheese"],
    values: ["Italy", "Iceland", "Thailand", "Switzerland"]
  },
  {
    text: "What scenery would you like to wake up to?",
    options: ["Views of rolling hills and vineyards", "Vast landscapes with glaciers", "Palm trees and turquoise waters", "Snow-capped mountains and pristine lakes"],
    values: ["Italy", "Iceland", "Thailand", "Switzerland"]
  }
];

const quizDiv = document.getElementById('quiz');
let currentQuestionIndex = 0;
const answers = {};

questions.forEach((question, index) => {
  const questionDiv = document.createElement('div');
  questionDiv.classList.add('question');
  questionDiv.innerHTML = `<p>${question.text}</p><ul>${question.options.map((option, optionIndex) => `<li onclick="selectOption(${index}, '${question.values[optionIndex]}')">${option}</li>`).join('')}</ul>`;
  quizDiv.appendChild(questionDiv);
});

function selectOption(questionIndex, value) {
  answers[questionIndex] = value;
  if (questionIndex + 1 < questions.length) {
    showQuestion(questionIndex + 1);
  } else {
    calculateDestination();
  }
}

function showQuestion(index) {
  const questionElements = document.querySelectorAll('.question');
  questionElements.forEach((element, i) => {
    element.style.display = i === index ? 'block' : 'none';
  });
}

function calculateDestination() {
  const destinationScores = { "Italy": 0, "Iceland": 0, "Thailand": 0, "Switzerland": 0 };
  Object.values(answers).forEach(answer => {
    destinationScores[answer] += 1;
  });
  const recommendedDestination = Object.keys(destinationScores).reduce((a, b) => destinationScores[a] > destinationScores[b] ? a : b);
  alert("Based on your answers, we recommend you travel to " + recommendedDestination + "!");
}

showQuestion(currentQuestionIndex);
</script>

</body>
</html>
