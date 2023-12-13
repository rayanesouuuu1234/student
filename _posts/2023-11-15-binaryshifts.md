---
comments: true
layout: notebook
title: Binary Shifting Demo
description: This demo shows how binary shifting works. Enter a number, choose a shift direction, and see the result in decimal and binary.
type: hacks
courses: { compsci: {week: 0} }
categories: [C4.1]
---

<html>
<head>

<style>
    body {
        
        font-family: 'Arial', sans-serif;
        background-color: #121212; /* Dark gray for less harsh contrast */
        color: #e0e0e0; /* Soft white for text */
        margin: 0;
        padding: 20px;
    }
    .form-container {
        background-color: #1e1e1e; /* Slightly lighter shade of dark gray */
        padding: 20px;
        border-radius: 8px;
        border: 1px solid #2a2a2a; /* Border color that stands out slightly */
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2); /* Subtle shadow for depth */
        max-width: 400px;
        margin: auto;
    }
    .form-group {
        margin-bottom: 15px;
    }
    label {
        display: block;
        margin-bottom: 5px;
        font-weight: bold;
        color: #e0e0e0; /* Soft white for labels */
    }
    input[type='number'], input[type='radio'], button {
        width: 100%;
        padding: 10px;
        margin-top: 5px;
        border: 1px solid #333; /* Dark border for input fields */
        border-radius: 4px;
        box-sizing: border-box;
        background-color: #262626; /* Dark input fields for contrast */
        color: #e0e0e0; /* Text color for input */
    }
    button {
        background-color: #3264a8; /* Less intense blue for the button */
        color: #ffffff;
        border: none;
        cursor: pointer;
    }
    button:hover {
        background-color: #2c4a8a; /* Darker blue on hover for interaction feedback */
    }
    .radio-group {
        display: flex;
        justify-content: start;
    }
    .radio-group label {
        margin: 0 10px 0 0;
        display: flex;
        align-items: center;
        color: #e0e0e0; /* Soft white for radio labels */
    }
    .radio-group input {
        width: auto;
        margin-right: 5px;
    }
    #result {
        margin-top: 20px;
        font-weight: bold;
        color: #4fc3f7; /* Lighter, more vibrant blue for results */
    }
</style>
</head>
<body>

    <!-- This is the main container for the form, styled with the 'form-container' class -->
    <div class="form-container">
        <!-- Container for the first group of form elements -->
        <div class="form-group">
            <!-- Label for the number input, associated with the input field by the 'for' attribute -->
            <label for="inputNumber">Enter a number to shift:</label>
            <!-- Numeric input field for entering the number, identified by 'id' -->
            <input type="number" id="inputNumber" placeholder="Enter a number">
        </div>
        <!-- Container for the second group of form elements -->
        <div class="form-group">
            <!-- Label for the shift amount input -->
            <label for="shiftAmount">Enter shift amount:</label>
            <!-- Numeric input field for entering the shift amount -->
            <input type="number" id="shiftAmount" placeholder="Shift amount">
        </div>
        <!-- Container for the third group of form elements -->
        <div class="form-group">
            <!-- Paragraph describing the next set of options -->
            <p>Select the direction of the shift:</p>
            <!-- Container for the radio buttons, styled with 'radio-group' -->
            <div class="radio-group">
                <!-- Radio button for selecting left shift, pre-selected with 'checked' attribute -->
                <label><input type="radio" id="leftShift" name="shiftDirection" value="left" checked> Left Shift (<<)</label>
                <!-- Radio button for selecting right shift -->
                <label><input type="radio" id="rightShift" name="shiftDirection" value="right"> Right Shift (>>)</label>
            </div>
        </div>
        <!-- Button to trigger the shift operation, calling 'performShift()' function on click -->
        <button onclick="performShift()">Shift</button>
        <!-- Paragraph element where the result will be displayed -->
        <p id="result"></p>
    </div>

    <script>
        // JS function that performs the shift
        function performShift() {
            // Retrieve the entered number from the input field
            var number = document.getElementById('inputNumber').value;
            // Retrieve the shift amount from the input field
            var shift = document.getElementById('shiftAmount').value;
            // Determine the direction of the shift based on the selected radio button
            var direction = document.querySelector('input[name="shiftDirection"]:checked').value;
            // Initialize the result variable
            var result = 0;
            // Perform the shift operation based on the indicated direction
            if (direction === 'left') {
                result = number << shift; // Left shift operation
            } else {
                result = number >> shift; // Right shift operation
            }

            // Display the result in binary format
            var binaryNumber = Number(number).toString(2);
            var binaryResult = Number(result).toString(2);

            // Display the result in the 'result' paragraph element
            document.getElementById('result').innerText = 'Result: ' +
                '\nDecimal: ' + result +
                '\nBinary: ' + binaryResult +
                '\n\nOriginal Number (Binary): ' + binaryNumber;
        }
    </script>

</body>
</html>
