---
toc: true
comments: true
layout: plans
title: Binary Shifting Demo
description: This demo shows how binary shifting works. Enter a number, choose a shift direction, and see the result.
type: hacks
courses: { csse: {week: 1}, csp: {week: 1, categories: [4.A]}, csa: {week: 0} }
---

<html>
<head>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .container {
            margin-bottom: 10px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input[type=number], button {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            box-sizing: border-box;
        }
        .radio-group {
            margin-bottom: 10px;
        }
        .radio-group label {
            margin-left: 5px;
        }
        #result {
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="container">
        <label for="inputNumber">Enter a number to shift:</label>
        <input type="number" id="inputNumber" placeholder="Enter a number" />
    </div>

    <div class="container">
        <label for="shiftAmount">Enter shift amount:</label>
        <input type="number" id="shiftAmount" placeholder="Shift amount" />
    </div>

    <p>Select the direction of the shift:</p>
    <div class="radio-group">
        <input type="radio" id="leftShift" name="shiftDirection" value="left" checked>
        <label for="leftShift">Left Shift (<<)</label>
        <input type="radio" id="rightShift" name="shiftDirection" value="right">
        <label for="rightShift">Right Shift (>>)</label>
    </div>

    <button onclick="performShift()">Shift</button>

    <p id="result"></p>

</body>
</html>
