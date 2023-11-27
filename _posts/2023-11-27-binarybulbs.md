---
toc: true
comments: true
layout: 
title: Binary Bulbs
description: Binary Bulbs program where 0s and 1s are represented by lightbulbs.
type: hacks
courses: { csse: {week: 1}, csp: {week: 1, categories: [4.A]}, csa: {week: 0} }
---
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Bulbs</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            margin: 20px;
        }

        h2 {
            color: #333;
        }

        .bulb-row {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 20px;
        }

        .bulb-box {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin: 10px;
        }

        .bulb {
            width: 50px;
            height: 50px;
            margin: 5px;
            cursor: pointer;
            background-size: cover;
            border: 2px solid #ccc;
            border-radius: 5px;
        }

        .bulb.on {
            background-image: url('https://imgs.search.brave.com/NXS21r_KAv6dNeXNdTdujnd_5G7oDYgvbnkPypQa_Gc/rs:fit:860:0:0/g:ce/aHR0cHM6Ly9jZG4t/MC5lbW9qaXMud2lr/aS9lbW9qaS1waWNz/L29wZW5tb2ppL2xp/Z2h0LWJ1bGItb3Bl/bm1vamkucG5n');
        }

        .bulb.off {
            background-image: url('https://imgs.search.brave.com/MFLjYBZxftkyeeaYWO-sjTk0MStDluO1SfkdWkly-ng/rs:fit:860:0:0/g:ce/aHR0cHM6Ly9jZG4t/aWNvbnMtcG5nLmZs/YXRpY29uLmNvbS81/MTIvMzIvMzIyOTku/cG5n'); 
        }

        .decimal-display {
            margin-top: 20px;
            font-size: 18px;
        }

        #turn-on-button {
            margin-top: 20px;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #turn-on-button:hover {
            background-color: #45a049;
        }
    </style>
</head>

<body>

    <h2>Binary Bulbs</h2>
    <label for="num-bulbs">Enter the number of bulbs: </label>
    <input type="number" id="num-bulbs" min="1" value="8">
    <button id="submit-button">Submit</button>

    <div class="bulb-row" id="bulbs-row"></div>
    <div class="decimal-display" id="decimal-display"></div>

    <script>
        function binaryBulbs(n) {
            return Array(n).fill(0);
        }

        function displayBulbs(bulbs) {
            const bulbsRow = document.getElementById('bulbs-row');
            bulbsRow.innerHTML = '';

            bulbs.forEach((bulb, index) => {
                const bulbBox = document.createElement('div');
                bulbBox.className = 'bulb-box';

                const bulbElement = document.createElement('div');
                bulbElement.className = 'bulb' + (bulb ? ' on' : ' off');

                // Add a click event listener to toggle the bulb's state on click
                bulbElement.addEventListener('click', () => {
                    bulbs[index] = 1 - bulbs[index];
                    displayBulbs(bulbs);
                    updateDecimalDisplay(bulbs);
                });

                bulbBox.appendChild(bulbElement);
                bulbsRow.appendChild(bulbBox);
            });
        }

        function updateDecimalDisplay(bulbs) {
            const decimalDisplay = document.getElementById('decimal-display');
            const decimalValue = parseInt(bulbs.join(''), 2);
            decimalDisplay.textContent = `Decimal: ${decimalValue}`;
        }

        document.addEventListener('DOMContentLoaded', function () {
            const numBulbsInput = document.getElementById('num-bulbs');
            const submitButton = document.getElementById('submit-button');

            submitButton.addEventListener('click', function () {
                const numBulbs = parseInt(numBulbsInput.value);

                if (!isNaN(numBulbs) && numBulbs > 0) {
                    const bulbsState = binaryBulbs(numBulbs);
                    displayBulbs(bulbsState);
                    updateDecimalDisplay(bulbsState);
                } else {
                    alert('Please enter a valid positive integer for the number of bulbs.');
                }
            });
        });
    </script>

</body>

</html>
