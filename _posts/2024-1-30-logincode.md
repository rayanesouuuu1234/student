---
title: JWT Login test (python/flask)
layout: base
description: A login screen that interacts with Python and obtains a JWT 
type: ccc
courses: { csp: {week: 18 }}
---
<form action="javascript:login_user()">
    <p><label>
        User ID:
        <input type="text" name="uid" id="uid" required>
    </label></p>
    <p><label>
        Password:
        <input type="password" name="password" id="password" required>
    </label></p>
    <p>
        <button>Login</button>
    </p>
</form>
<!--
Javascript code to handle user authentication in web aapplicaation.
-->
<script type="module">
    import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';
    function login_user(){
        const url = uri + '/api/users/authenticate';
        const body = {
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
        };
        const authOptions = {
            ...options, 
            method: 'POST', 
            cache: 'no-cache',
            body: JSON.stringify(body)
        };
        // Fetch JWT
        fetch(url, authOptions)
        .then(response => {
            // handle error response from Web API
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // redirect to database page
            window.location.href = "{{site.baseurl}}/data/database";
        })
        // catch fetch errors
        .catch(err => {
            console.error(err);
        });
    }
    window.login_user = login_user;
</script>