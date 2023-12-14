<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Number Guesser</title>
    <style>
        body {
            font-family: 'Courier New', Courier, monospace;
            text-align: center;
            margin: 20px;
            background: url('https://cf.geekdo-images.com/fv4bK3hKcaHneY-e7SRNjA__opengraph/img/ymistn_5KhQNb1PuDssJ2jOr208=/0x6:609x339/fit-in/1200x630/filters:fill(blur):strip_icc()/pic6367073.jpg') center center fixed;
            background-size: cover;
            padding-top: 70px; /* Adjusted padding for the top bar */
        }
        h1 {
            color: #333;
            margin-bottom: 20px;
        }
        #legend {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 70px;
            display: flex;
            justify-content: space-between;
            padding: 10px;
            background-color: rgba(255, 255, 255, 0.8);
            z-index: 1;
        }
        .legend-item {
            flex: 1;
            text-align: center;
            font-size: 14px;
        }
        #game-container {
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            margin: 0 auto;
            color: black;
            margin-top: 80px; /* Adjusted margin to accommodate the legend bar */
        }
        label {
            display: block;
            margin-bottom: 10px;
        }
        input {
            padding: 10px;
            margin-bottom: 20px;
            width: 100%;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            width: 100%;
            border-radius: 5px;
        }
        button:hover {
            background-color: #45A049;
        }
        #resultMessage, #loadingScreen p, #game-container p {
            color: black;
        }
        #loadingScreen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255, 255, 255, 0.8);
            justify-content: center;
            align-items: center;
        }
    </style>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guess the Binary Number</title>
</head>
<body>
<div id="legend">
    <div class="legend-item" style="background-color: #ADD8E6;">+/- 2</div>
    <div class="legend-item" style="background-color: #90EE90;">+/- 4</div>
    <div class="legend-item" style="background-color: #FFA500;">+/- 6</div>
    <div class="legend-item" style="background-color: #FF0000;">+/- 8</div>
</div>
<div id="loadingScreen">
    <p>Loading...</p>
</div>
<div id="game-container">
    <label for="guessInput">Enter your guess (a binary number):</label>
    <input type="text" id="guessInput" placeholder="Enter binary number" autocomplete="off">
    <button onclick="checkNumber()">Check Number</button>
    <p id="resultMessage"></p>
</div>
<script>
    let attempts = 0;
    const maxAttempts = 3;
    function getRandomBinaryNumber() {
        let randomNumber = Math.floor(Math.random() * 16);
        return randomNumber.toString(2).padStart(4, '0');
    }
    function showLoadingScreen() {
        document.getElementById('loadingScreen').style.display = 'flex';
        setTimeout(hideLoadingScreen, 5000); // 5 seconds
    }
    function hideLoadingScreen() {
        document.getElementById('loadingScreen').style.display = 'none';
    }
    function checkNumber() {
        const guessInput = document.getElementById('guessInput');
        const resultMessage = document.getElementById('resultMessage');
        const guess = guessInput.value.trim();  // Trim to remove leading/trailing whitespaces
        const correctAnswer = getRandomBinaryNumber();
        if (attempts >= maxAttempts) {
            resultMessage.textContent = `Sorry, you've reached the maximum number of attempts. The correct binary number was: ${correctAnswer}`;
            return;
        }
        showLoadingScreen();
        setTimeout(function () {
            attempts++;
            if (guess === correctAnswer) {
                resultMessage.textContent = `Congratulations! You guessed the correct binary number: ${correctAnswer}`;
            } else {
                resultMessage.textContent = 'Wrong Answer!';
            }
            if (attempts >= maxAttempts) {
                resultMessage.textContent = `Sorry, you've reached the maximum number of attempts. The correct binary number was: ${correctAnswer}`;
            }
            hideLoadingScreen();
        }, 5000);
    }
</script>
</body>
</html>