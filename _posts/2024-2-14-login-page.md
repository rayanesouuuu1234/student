<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login Page</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f0f8ff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    form {
      background: #ffffff;
      padding: 40px;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s ease-in-out;
    }
    form:hover {
      transform: scale(1.02);
    }
    label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }
    input[type="text"], input[type="password"] {
      width: 100%;
      padding: 10px;
      margin: 10px 0 20px;
      border: 1px solid #ddd;
      border-radius: 4px;
      box-sizing: border-box;
      transition: border-color 0.3s ease-in-out;
    }
    input[type="text"]:focus, input[type="password"]:focus {
      border-color: #007bff;
      outline: none;
    }
    button {
      padding: 10px 15px;
      border: none;
      border-radius: 4px;
      background-color: #007bff;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s ease-in-out;
    }
    button:hover {
      background-color: #0056b3;
    }
    .button-spacing {
      margin-right: 10px;
    }
    #errorMessage {
      color: red;
      text-align: center;
    }
  </style>
</head>
<body>
  <div id="errorMessage"></div>
  <form>
    <p>
      <label for="uid">User ID:</label>
      <input type="text" name="uid" id="uid" required>
    </p>
    <p>
      <label for="password">Password:</label>
      <input type="password" name="password" id="password" required>
    </p>
    <p>
      <button type="button" class="button-spacing" onclick="login_user()">Log In</button>
      <button type="button" onclick="window.location.href='https://rayanesouuuu1234.github.io/tri2/2024/02/12/signup.html'" class="button-spacing">Sign Up</button>
    </p>
  </form>

  <script>
    function login_user() {
      console.log("login_user function called"); 
      const enteredUid = document.getElementById("uid").value;
      const enteredPassword = document.getElementById("password").value;
      console.log("Uid = " + enteredUid)
      console.log("Password = " + enteredPassword)
      login_api(enteredUid, enteredPassword); 
    }

    async function login_api(uid, password) { 
      console.log("login_api function called"); 
      var myHeaders = new Headers();
      myHeaders.append("Accept", "*/*");
      myHeaders.append("Accept-Language", "en-US,en;q=0.9");
      myHeaders.append("Content-Type", "application/json");
      myHeaders.append("Cookie", "jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJfdWlkIjoidG9ueSJ9.jEShka0oXI1-uCuSTfo3ed5WRw3ASLNV0Tpn1kc5GB0");
      
      var raw = JSON.stringify({
        "uid": uid, 
        "password": password 
      });

      var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };

      try {
        const response = await fetch("http://127.0.0.1:8086/api/users/authenticate", requestOptions);
        console.log("Response received:", response); 

        if (response.ok) {
          console.log("User logged in successfully");
          alert("Login Successful!!");
          window.location.href = "https://rayanesouuuu1234.github.io/cpt_frontend/2024/02/12/Home-Page.html";
        } else {
          console.error("User login failed");
          alert("Login Unsuccessful");
          const errorMessageDiv = document.getElementById('errorMessage');
          errorMessageDiv.innerHTML = '<label style="color: red;">User Login Failed</label>';
        }
      } catch (error) {
        console.error('Error:', error);
        alert("An error occurred during login: " + error.message); // Displaying the error message
      }
    }
  </script>
</body>
</html>
