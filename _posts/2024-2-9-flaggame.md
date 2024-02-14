---
toc: true
comments: true
layout: 
title: Flag Guess Game
description:
type: hacks
courses: { csse: {week: 1}, csp: {week: 1, categories: [4.A]}, csa: {week: 0} }
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flag Guessing Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            text-align: center;
            background-image: url('https://imagecache.jpl.nasa.gov/images/edu/images/imagerecords/57000/57723/globe_west_2048-640x350.jpg');
            background-size: cover;
            background-position: center;
            display: flex; 
            align-items: center; 
            justify-content: center; 
            height: 100vh; 
        }
        .homepage {
            max-width: 400px;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }
        .homepage h1 {
            color: #333;
            margin-bottom: 20px;
        }
        .button {
            display: inline-block;
            margin: 10px;
            padding: 10px 20px;
            background-color: #c3d7ff;
            border: 2px solid blue;
            border-radius: 5px;
            cursor: pointer;
            text-decoration: none;
            color: #333;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        .button:hover {
            background-color: #b0c5f5;
        }
        #quiz-container {
            max-width: 600px;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.8); 
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); 
        }
        h1 {
            color: #333;
        }
        #question {
            font-size: 20px;
            margin-bottom: 20px;
        }
        .option {
            display: inline-block;
            margin: 5px;
            padding: 10px 20px;
            background-color: #c3d7ff; 
            border: 2px solid blue;
            cursor: pointer;
        }
        .option:hover {
            background-color: #b0c5f5;
        }
        #score {
            margin-top: 20px;
            font-size: 18px;
            color: #666;
        }
        .blue-box {
            padding: 10px;
            margin-bottom: 20px;
            display: inline-block;
        }
        #ending-screen {
            display: none; 
            background-color: rgba(255, 255, 255, 0.8); 
            padding: 20px;
            border-radius: 10px;
            max-width: 400px; 
        }
    </style>
</head>
<body>
    <div class="homepage">
        <h1>Welcome to the Flag Guessing Quiz</h1>
        <a href="#" class="button" onclick="startGame()">Play Game</a>
        <a href="https://rayanesouuuu1234.github.io/tri2/2024/02/09/flaglist.html" class="button">List of Flags</a>
    </div>
    
    <div id="quiz-container" style="display: none;">
        <h1>Flag Guessing Quiz</h1>
        <div id="question"></div>
        <div class="blue-box">
            <div id="flag-image"></div>
            <div id="options"></div>
        </div>
        <div id="score">Score: <span id="current-score">0</span>/10</div>
    </div>

    <div id="ending-screen">
        <div style="background-color: rgba(255, 255, 255, 0.8); padding: 20px; border-radius: 10px;">
            <h1>Quiz Finished!</h1>
            <div>Your total score is <span id="total-score"></span>/10</div>
            <button id="play-again-button" onclick="resetQuiz()">Play Again</button>
        </div>
    </div>
    <script>
        let currentQuestionIndex = 0;
        let score = 0;

        const questionElement = document.getElementById('question');
        const optionsElement = document.getElementById('options');
        const scoreElement = document.getElementById('current-score');
        const endingScreen = document.getElementById('ending-screen');
        const totalScoreElement = document.getElementById('total-score');

        async function fetchFlagData() {
            try {
                const response = await fetch('https://restcountries.com/v3.1/all');
                const data = await response.json();
                return data;
            } catch (error) {
                console.error('Error fetching flag data:', error);
            }
        }

        function getRandomQuestion(data) {
            const randomIndex = Math.floor(Math.random() * data.length);
            const country = data[randomIndex];
            const flag = country.flags.png;
            const name = country.name.common;
            const options = getRandomOptions(data, country);

            return {
                flag,
                name,
                options
            };
        }

        function getRandomOptions(data, country) {
            const options = [country.name.common];
            while (options.length < 5) {
                const randomIndex = Math.floor(Math.random() * data.length);
                const option = data[randomIndex].name.common;
                if (!options.includes(option)) {
                    options.push(option);
                }
            }
            return shuffleArray(options);
        }

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        async function loadQuestion() {
            const flagData = await fetchFlagData();
            const { flag, name, options } = getRandomQuestion(flagData);
            questionElement.textContent = `Which country does this flag belong to?`;
            document.getElementById('flag-image').innerHTML = `<img src="${flag}" alt="Flag">`;
            optionsElement.innerHTML = options.map(option => `
                <div class="option" onclick="checkAnswer('${option}', '${name}')">${option}</div>
            `).join('');
        }

        function checkAnswer(selectedOption, correctOption) {
            if (selectedOption === correctOption) {
                score++;
                scoreElement.textContent = score;
            }
            currentQuestionIndex++;
            if (currentQuestionIndex < 10) {
                loadQuestion();
            } else {
                showEndingScreen();
            }
        }

        function showEndingScreen() {
            document.getElementById('quiz-container').style.display = 'none';
            endingScreen.style.display = 'block';
            totalScoreElement.textContent = score;
        }

        function resetQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            scoreElement.textContent = score;
            endingScreen.style.display = 'none';
            document.getElementById('quiz-container').style.display = 'block';
            loadQuestion();
        }

        function startGame() {
            document.querySelector('.homepage').style.display = 'none';
            document.getElementById('ending-screen').style.display = 'none';
        
            document.getElementById('quiz-container').style.display = 'block';
        
            loadQuestion();
        }

        loadQuestion();
    </script>
</body>
</html>
