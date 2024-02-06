---
toc: true
comments: true
layout: 
title: login page
description:
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
            background: #000;
            color: #fff;
        }

        .form-container {
            background: #222;
            padding: 20px 40px;
            border-radius: 5px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
            text-align: center;
        }

        h2 {
            margin-bottom: 20px;
            color: #fff;
            font-size: 24px;
        }

        label {
            display: block;
            text-align: left;
            margin: 4px 0;
            color: #bbb;
            font-size: 14px;
        }

        input[type="text"],
        input[type="password"] {
            width: 100%;
            padding: 8px 12px;
            margin-bottom: 15px;
            border: 1px solid #333;
            background: #333;
            color: #fff;
            border-radius: 4px;
            box-sizing: border-box;
            transition: border-color 0.3s;
        }

        input[type="text"]:focus,
        input[type="password"]:focus {
            border-color: #555;
            box-shadow: none;
        }

        button {
            width: 100%;
            padding: 10px 0;
            border: none;
            border-radius: 4px;
            background: #333;
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background: #444;
        }

        .register-btn {
            background: #444;
            margin-top: 8px;
        }

        .form-footer {
            margin-top: 15px;
            font-size: 14px;
            color: #aaa;
        }

        .form-footer a {
            color: #999;
            text-decoration: none;
            transition: color 0.3s;
        }

        .form-footer a:hover {
            color: #bbb;
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
    e.preventDefault();

    const loginData = {
        uid: document.getElementById('loginUsername').value,
        password: document.getElementById('loginPassword').value,
    };

    fetch('http://127.0.0.1:8086/api/users/authenticate', {
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
        return response.json();
    })
    .then(data => {
        console.log(data);
        alert('Login successful! Redirecting...');
        window.location.href = 'game.html';
    })
    .catch(error => {
        console.error('There was a problem with the login operation:', error);
        alert('Failed to log in: ' + error.message);
        document.getElementById('loginUsername').value = '';
        document.getElementById('loginPassword').value = '';
    });
});

document.getElementById('goToSignup').addEventListener('click', function() {
    window.location.href = 'signup.html';
});
</script>

</body>
</html>
