---
toc: true
comments: true
layout: 
title: Binary guessing game
description: The player has to guess a random binary number made by the computer.
type: hacks
courses: { csse: {week: 1}, csp: {week: 1, categories: [4.A]}, csa: {week: 0} }
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Binary Guessing Game</title>
</head>
<body>

<script>
  // Function to generate a random binary number
  function generateRandomBinary() {
    let binaryNumber = '';
    for (let i = 0; i < 4; i++) {
      binaryNumber += Math.round(Math.random());
    }
    return binaryNumber;
  }

  // Function to convert binary to decimal
  function binaryToDecimal(binary) {
    return parseInt(binary, 2);
  }

  // Main game function
  function playGame() {
    // Generate a random binary number
    const randomBinary = generateRandomBinary();

    // Ask the player to guess the decimal equivalent
    const playerGuess = prompt(`Guess the decimal equivalent of ${randomBinary}:`);

    // Convert the binary number to decimal for comparison
    const decimalEquivalent = binaryToDecimal(randomBinary);

    // Check if the player's guess is correct
    if (parseInt(playerGuess) === decimalEquivalent) {
      alert(`Congratulations! You guessed it right. The decimal equivalent of ${randomBinary} is ${decimalEquivalent}.`);
    } else {
      alert(`Sorry, that's incorrect. The correct decimal equivalent of ${randomBinary} is ${decimalEquivalent}.`);
    }
    const playAgain = confirm("Do you want to play again?");
    if (playAgain) {
      playGame(); // Restart the game
    } else {
      alert("Thanks for playing! Goodbye.");
    }
  }

  // Start the game
  playGame();
</script>

</body>
</html>

