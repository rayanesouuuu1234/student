---
toc: true
comments: true
layout: 
title: login page
description: Homepage for users to access all programs at one site.
type: hacks
courses: { csse: {week: 1}, csp: {week: 1, categories: [4.A]}, csa: {week: 0} }
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
    <style>
        body, html {
            height: 100%;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
            background: #000; /* Changed to black */
            color: #fff; /* Adjusted for contrast */
        }

        .form-container {
            background: #222; /* Darker background for the form */
            padding: 20px 40px; /* Adjusted padding for sleekness */
            border-radius: 5px; /* Smoother edges */
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5); /* Subtle shadow */
            text-align: center;
        }

        h2 {
            margin-bottom: 20px; /* Adjusted spacing */
            color: #fff; /* Brighter text for readability */
            font-size: 24px; /* Smaller for sleekness */
        }

        label {
            display: block;
            text-align: left;
            margin: 4px 0;
            color: #bbb; /* Lighter text color for visibility */
            font-size: 14px;
        }

        input[type="text"],
        input[type="password"] {
            width: 100%;
            padding: 8px 12px; /* Adjusted for sleekness */
            margin-bottom: 15px; /* Reduced gap */
            border: 1px solid #333; /* Subtler border */
            background: #333; /* Darker input background */
            color: #fff; /* Text color for inputs */
            border-radius: 4px; /* Sleeker border radius */
            box-sizing: border-box;
            transition: border-color 0.3s;
        }

        input[type="text"]:focus,
        input[type="password"]:focus {
            border-color: #555; /* Focus color */
            box-shadow: none; /* Removed for sleekness */
        }

        button {
            width: 100%;
            padding: 10px 0; /* Adjusted padding */
            border: none;
            border-radius: 4px; /* Consistent rounding */
            background: #333; /* Darker buttons */
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background: #444; /* Hover effect */
        }

        .register-btn {
            background: #444; /* Differentiated register button */
            margin-top: 8px; /* Adjusted spacing */
        }

        .form-footer {
            margin-top: 15px; /* Adjusted spacing */
            font-size: 14px;
            color: #aaa; /* Lighter for visibility */
        }

        .form-footer a {
            color: #999; /* Subtle link color */
            text-decoration: none;
            transition: color 0.3s;
        }

        .form-footer a:hover {
            color: #bbb; /* Hover effect */
        }
    </style>
</head>
<body>

<div class="form-container">
    <form id="loginForm">
        <h2>Welcome Back!</h2>
        <label for="loginUsername">Username:</label>
        <input type="text" id="loginUsername" name="loginUsername" required>
        <label for="loginPassword">Password:</label>
        <input type="password" id="loginPassword" name="loginPassword" required>
        <button type="submit">Log In</button>
        <button type="button" class="register-btn" id="goToSignup">Register</button>
        <div class="form-footer">
            <a href="#">Forgot your password?</a>
        </div>
    </form>
</div>

<script>
document.getElementById('loginForm').addEventListener('submit', function(e) {
    e.preventDefault(); // Prevent default form submission

    const loginData = {
        uid: document.getElementById('loginUsername').value,
        password: document.getElementById('loginPassword').value,
    };

    fetch('http://127.0.0.1:8086/api/users/authenticate', { // Adjust the endpoint if necessary
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(loginData),
    })
    .then(response => {
        if (!response.ok) {
            throw new Error('Login failed: ' + response.statusText);
        }
        return response.json(); // Assuming the server responds with JSON
    })
    .then(data => {
        // Handle successful login here
        console.log(data); // You might want to use the data for something
        alert('Login successful! Redirecting...');
        window.location.href = 'game.html'; // Redirect to another page on success
    })
    .catch(error => {
        // Handle login errors here
        console.error('There was a problem with the login operation:', error);
        alert('Failed to log in: ' + error.message);
        // Clear input fields if login fails
        document.getElementById('loginUsername').value = '';
        document.getElementById('loginPassword').value = '';
    });
});

document.getElementById('goToSignup').addEventListener('click', function() {
    window.location.href = 'signup.html'; // Replace 'signup.html' with your signup page URL
});
</script>

</body>
</html>
