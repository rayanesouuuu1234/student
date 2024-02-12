<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trivia Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }

        #question {
            font-size: 1.5em;
            margin-bottom: 20px;
        }

        #options {
            display: flex;
            justify-content: center;
        }

        button {
            font-size: 1em;
            margin: 10px;
            padding: 10px 20px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Trivia Game</h1>
    <div id="question"></div>
    <div id="options"></div>
    
    <script>
        // Function to fetch trivia questions from the Open Trivia Database API
        async function fetchTriviaQuestions() {
            const response = await fetch('https://opentdb.com/api.php?amount=1&type=multiple');
            const data = await response.json();
            return data.results[0];
        }

        // Function to display the question and answer options
        function displayQuestion(question) {
            const questionElement = document.getElementById('question');
            const optionsElement = document.getElementById('options');
            
            questionElement.textContent = question.question;

            // Combine incorrect and correct answer options
            const allOptions = question.incorrect_answers.concat(question.correct_answer);

            // Shuffle the options
            const shuffledOptions = allOptions.sort(() => Math.random() - 0.5);

            // Display options as buttons
            optionsElement.innerHTML = '';
            shuffledOptions.forEach(option => {
                const button = document.createElement('button');
                button.textContent = option;
                button.addEventListener('click', () => checkAnswer(option, question.correct_answer));
                optionsElement.appendChild(button);
            });
        }

        // Function to check the selected answer
        function checkAnswer(selectedAnswer, correctAnswer) {
            if (selectedAnswer === correctAnswer) {
                alert('Correct!');
            } else {
                alert(`Wrong! The correct answer is: ${correctAnswer}`);
            }

            // Fetch a new question after answering
            fetchNewQuestion();
        }

        // Function to fetch a new question and display it
        async function fetchNewQuestion() {
            const question = await fetchTriviaQuestions();
            displayQuestion(question);
        }

        // Initial setup - fetch and display the first question
        fetchNewQuestion();
    </script>
</body>
</html>