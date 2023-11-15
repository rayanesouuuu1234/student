---
toc: true
comments: true
layout: notebook  # Assuming 'post' is a valid layout in your setup.
title: Binary Shifting Demo
description: This demo shows how binary shifting works. Enter a number, choose a shift direction, and see the result.
type: hacks
courses: 
  csse: {week: 1}
  csp: {week: 1, categories: [4.A]}
  csa: {week: 0}
---

<html>
<head>
    <title>Binary Shifting Demo</title>
    <style>
        /* Add your CSS styles here if needed */
    </style>
    <script>
        // JavaScript function to perform binary shifting
        function performShift() {
            // Read input values from the form
            var inputNumber = parseInt(document.getElementById('inputNumber').value, 10);
            var shiftAmount = parseInt(document.getElementById('shiftAmount').value, 10);

            if (isNaN(inputNumber) || isNaN(shiftAmount)) {
                alert("Please enter valid numbers");
                return;
            }

            var shiftDirection = document.querySelector('input[name="shiftDirection"]:checked').value;

            var result;
            // Perform the shifting operation
            if (shiftDirection === 'left') {
                result = inputNumber << shiftAmount;
            } else {
                result = inputNumber >> shiftAmount;
            }

            // Display the result
            document.getElementById('result').innerText = 'Result: ' + result.toString(2);
        }
    </script>
</head>
<body>
    <h2>Binary Shifting Demo</h2>
    <p>This demo shows how binary shifting works. Enter a number, choose a shift direction, and see the result.</p>
    
    <!-- User input for the number to shift -->
    <label for="inputNumber">Enter a number to shift:</label>
    <input type="number" id="inputNumber" placeholder="Enter a number" />
    
    <!-- User input for the shift amount -->
    <label for="shiftAmount">Enter shift amount:</label>
    <input type="number" id="shiftAmount" placeholder="Shift amount" />

    <p>Select the direction of the shift:</p>
    <div>
        <!-- Option to choose left shift -->
        <input type="radio" id="leftShift" name="shiftDirection" value="left" checked>
        <label for="leftShift">Left Shift (<<)</label>

        <!-- Option to choose right shift -->
        <input type="radio" id="rightShift" name="shiftDirection" value="right">
        <label for="rightShift">Right Shift (>>)</label>
    </div>
    
    <!-- Button to perform the shift -->
    <button onclick="performShift()">Shift</button>

    <!-- Display the result of the shift -->
    <p id="result"></p>
</body>
</html>
