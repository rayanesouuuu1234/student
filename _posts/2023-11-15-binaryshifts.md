---
comments: true
layout: notebook
title: Binary Shifting Demo
description: This demo shows how binary shifting works. Enter a number, choose a shift direction, and see the result.
type: hacks
courses: { compsci: {week: 0} }
categories: [C4.1]
---

<html>
<head>
<style>
    body {
        font-family: 'Arial', sans-serif;
        background-color: #121212;
        color: #e0e0e0;
        margin: 0;
        padding: 20px;
    }
    .form-container {
        background-color: #1e1e1e;
        padding: 20px;
        border-radius: 8px;
        border: 1px solid #2a2a2a;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
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
    }
    input[type='number'], input[type='radio'], button {
        width: 100%;
        padding: 10px;
        margin-top: 5px;
        border: 1px solid #333;
        border-radius: 4px;
        box-sizing: border-box;
        background-color: #262626;
        color: #e0e0e0;
    }
    button {
        background-color: #3264a8;
        color: #ffffff;
        border: none;
        cursor: pointer;
    }
    button:hover {
        background-color: #2c4a8a;
    }
    .radio-group {
        display: flex;
        justify-content: start;
    }
    .radio-group label {
        margin: 0 10px 0 0;
        display: flex;
        align-items: center;
    }
    .radio-group input {
        width: auto;
        margin-right: 5px;
    }
    #result, #binaryBefore, #binaryAfter {
        margin-top: 20px;
        font-weight: bold;
        color: #4fc3f7;
    }
</style>
</head>
<body>

<div class="form-container">
    <div class="form-group">
        <label for="inputNumber">Enter a number to shift:</label>
        <input type="number" id="inputNumber" placeholder="Enter a number">
    </div>
    <div class="form-group">
        <label for="shiftAmount">Enter shift amount:</label>
        <input type="number" id="shiftAmount" placeholder="Shift amount">
    </div>
    <div class="form-group">
        <p>Select the direction of the shift:</p>
        <div class="radio-group">
            <label><input type="radio" id="leftShift" name="shiftDirection" value="left" checked> Left Shift (<<)</label>
            <label><input type="radio" id="rightShift" name="shiftDirection" value="right"> Right Shift (>>)</label>
        </div>
    </div>
    <button onclick="performShift()">Shift</button>
    <p id="binaryBefore"></p>
    <p id="result"></p>
    <p id="binaryAfter"></p>
</div>

<script>
// JavaScript function to perform binary shifts and demonstrate binary logic
// Functionality enhanced by Team Member 1: Binary shift operation
// Functionality enhanced by Team Member 2: Binary conversion algorithm

function toBinary(number) {
    return (number >>> 0).toString(2);
}

function performShift() {
    var number = parseInt(document.getElementById('inputNumber').value);
    var shift = parseInt(document.getElementById('shiftAmount').value);
    var direction = document.querySelector('input[name="shiftDirection"]:checked').value;

    document.getElementById('binaryBefore').innerText = 'Binary before shift: ' + toBinary(number);

    var result = 0;
    if (direction === 'left') {
        result = number << shift;
    } else {
        result = number >> shift;
    }

    document.getElementById('binaryAfter').innerText = 'Binary after shift: ' + toBinary(result);
    document.getElementById('result').innerText = 'Decimal Result: ' + result;
}
</script>

</body>
</html>