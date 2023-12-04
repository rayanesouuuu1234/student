---
toc: true
comments: true
layout: 
title: Binary Quiz
description: Program that quizzes users on binary and keeps track of theit score.
type: hacks
courses: { csse: {week: 1}, csp: {week: 1, categories: [4.A]}, csa: {week: 0} }
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      font-family: 'Arial', sans-serif;
      background-color: #f4f4f4;
    }

    #quiz-container {
      text-align: center;
      background-color: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    #question {
      font-size: 24px;
      margin-bottom: 20px;
      color: #333;
    }

    #input {
      font-size: 18px;
      padding: 10px;
      margin-bottom: 20px;
      width: 200px;
    }

    #result {
      font-size: 18px;
      color: green;
      margin-bottom: 10px;
    }

    #score {
      font-size: 20px;
      font-weight: bold;
      margin-top: 20px;
      color: #555;
    }

    #check-answer-btn {
      font-size: 18px;
      padding: 12px 20px;
      cursor: pointer;
      background-color: #87CEFA;
      color: #fff;
      border: none;
      border-radius: 4px;
    }
    
  </style>
  <title>Binary Quiz</title>
</head>
<body>
  <div id="quiz-container">
    <div id="question"></div>
    <input type="text" id="input" placeholder="Enter your answer">
    <div id="result"></div>
    <div id="score"></div>
    <button id="check-answer-btn" onclick="checkAnswer()">Check Answer & Next Question</button>
  </div>

  <script>
    document.addEventListener('DOMContentLoaded', function () {
      const quizContainer = document.getElementById('quiz-container');
      const questionElement = document.getElementById('question');
      const inputElement = document.getElementById('input');
      const resultElement = document.getElementById('result');
      const scoreElement = document.getElementById('score');
      const checkAnswerBtn = document.getElementById('check-answer-btn');
      let totalQuestions = 0;
      let correctAnswers = 0;

      function generateRandomBinary() {
        const binaryValue = Math.floor(Math.random() * 256).toString(2);
        return binaryValue.padStart(8, '0');
      }

      function generateQuestion() {
        const binaryNumber = generateRandomBinary();
        questionElement.textContent = `Convert ${binaryNumber} to decimal`;
        inputElement.value = '';
        resultElement.textContent = '';
        updateScore(); // Display the current score
      }

      window.checkAnswer = function () {
        const binaryNumber = questionElement.textContent.split('Convert ')[1].split(' to decimal')[0];
        const userAnswer = inputElement.value.trim();
        const correctAnswer = parseInt(binaryNumber, 2);

        if (userAnswer === correctAnswer.toString()) {
          resultElement.textContent = 'Correct!';
          correctAnswers++;
        } else {
          resultElement.textContent = `Incorrect. The correct answer is ${correctAnswer}`;
        }

        totalQuestions++;
        updateScore(); // Display the current score
        generateQuestion(); // Move to the next question
      };

      function updateScore() {
        scoreElement.textContent = `${correctAnswers}/${totalQuestions}`;
      }

      generateQuestion(); // Initial question generation
    });
  </script>
</body>
</html>
