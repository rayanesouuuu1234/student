---
toc: true
comments: true
layout: 
title: Binary Color Wheel
description: Color wheel that takes user binary input and displays a color
type: hacks
courses: { csse: {week: 1}, csp: {week: 1, categories: [4.A]}, csa: {week: 0} }
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Color Wheel</title>
    <style>
        body {
            font-family: 'Helvetica', 'Arial', sans-serif;
            background-color: #f8f9fa;
            margin: 20px;
            text-align: center;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-size: 14px;
            color: #495057;
        }

        input {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            margin-bottom: 10px;
            border: 1px solid #ced4da;
            border-radius: 4px;
            font-size: 14px;
        }

        #colorDisplay {
            width: 100px;
            height: 100px;
            border: 1px solid #343a40;
            margin: 10px auto;
        }

        button {
            padding: 10px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <label for="redBinary">Red (8-bit binary):</label>
    <input type="text" id="redBinary" maxlength="8" pattern="[01]{8}" required>
    
    <label for="greenBinary">Green (8-bit binary):</label>
    <input type="text" id="greenBinary" maxlength="8" pattern="[01]{8}" required>
    
    <label for="blueBinary">Blue (8-bit binary):</label>
    <input type="text" id="blueBinary" maxlength="8" pattern="[01]{8}" required>
    
    <label for="colorPicker">Choose a color:</label>
    <input type="color" id="colorPicker" value="#000000">
    
    <br>
    
    <button onclick="displayColor()">Display Color</button>
    
    <div id="colorDisplay"></div>

    <script>
        function binaryToDecimal(binaryStr) {
            return parseInt(binaryStr, 2);
        }

        function updateBinaryValues(color) {
            var red = color >> 16 & 0xFF;
            var green = color >> 8 & 0xFF;
            var blue = color & 0xFF;

            document.getElementById("redBinary").value = red.toString(2).padStart(8, '0');
            document.getElementById("greenBinary").value = green.toString(2).padStart(8, '0');
            document.getElementById("blueBinary").value = blue.toString(2).padStart(8, '0');
        }

        function displayColor() {
            var redBinary = document.getElementById("redBinary").value;
            var greenBinary = document.getElementById("greenBinary").value;
            var blueBinary = document.getElementById("blueBinary").value;

            if (!/^[01]{8}$/.test(redBinary) || !/^[01]{8}$/.test(greenBinary) || !/^[01]{8}$/.test(blueBinary)) {
                alert("Invalid binary input. Please enter a valid 8-bit binary string.");
                return;
            }

            var red = binaryToDecimal(redBinary);
            var green = binaryToDecimal(greenBinary);
            var blue = binaryToDecimal(blueBinary);

            var colorDisplay = document.getElementById("colorDisplay");
            colorDisplay.style.backgroundColor = "rgb(" + red + "," + green + "," + blue + ")";
        }

        // Add event listener for color picker change
        document.getElementById("colorPicker").addEventListener("input", function () {
            var color = parseInt(this.value.substring(1), 16); // Convert hex to decimal
            updateBinaryValues(color);
            displayColor();
        });

        // Initialize binary values and color display on page load
        updateBinaryValues(parseInt(document.getElementById("colorPicker").value.substring(1), 16));
        displayColor();
    </script>
</body>
</html>
