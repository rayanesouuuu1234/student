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
    options: ["Sunny and Mediterranean", "Mild and temperate", "Hot and sunny"],
    values: ["City", "National Park", "Tropical"]
  },
  {
    text: "What activity sounds most appealing to you?",
    options: ["Sightseeing and shopping", "Hiking and outdoor adventures", "Relaxing on the beach"],
    values: ["City", "National Park", "Tropical"]
  },
  {
    text: "What type of landscape do you find most appealing?",
    options: ["Skyscrapers and urban scenery", "Mountains and forests", "Palm trees and beaches"],
    values: ["City", "National Park", "Tropical"]
  },
  {
    text: "How do you like to spend your evenings?",
    options: ["Exploring nightlife and dining out", "Stargazing and bonfires", "Watching the sunset by the ocean"],
    values: ["City", "National Park", "Tropical"]
  },
  {
    text: "What kind of cuisine are you most interested in trying?",
    options: ["International cuisine and gourmet dining", "Local specialties cooked over a campfire", "Fresh seafood and exotic fruits"],
    values: ["City", "National Park", "Tropical"]
  },
  {
    text: "What is your preferred mode of transportation?",
    options: ["Public transportation and taxis", "Hiking or biking", "Relaxing in a hammock or on a boat"],
    values: ["City", "National Park", "Tropical"]
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
  const destinationScores = { "City": 0, "National Park": 0, "Tropical": 0};
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
