<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login Page</title>
  <link rel="stylesheet" href="styles.css">
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
      <button onclick="window.location.href='https://rayanesouuuu1234.github.io/tri2/2024/01/31/signup.html'" class="button-spacing">Sign Up</button>
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
          window.location.href = "http://127.0.0.1:4000/tri2/2024/01/31/game.html";
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
