---
toc: False
layout: post
hide: False
title: post
courses: {timebox: {week: 3}}
permalink: login
type: hacks
---
<!-- 
A simple HTML login form with a Login action when button is pressed.  

The form triggers the login_user function defined in the JavaScript below when the Login button is pressed.
-->

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #ffffff;
            background-image: url("https://paintings.pinotspalette.com/moonlit-cherry-blossom-river-hdtv.jpeg?v=10039310");
            margin: 0;
            padding: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        h2 {
            text-align: center;
            color: #333;
        }

        form {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 16px;
            box-sizing: border-box;
        }

        input[type="submit"] {
            background-color: #4caf50;
            color: #fff;
            cursor: pointer;
        }

        input[type="submit"]:hover {
            background-color: #45a049;
        }

        p {
            text-align: center;
            margin-top: 16px;
            color: #555;
        }

        a {
            color: #4caf50;
            text-decoration: none;
        }

        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <form action="javascript:login_user()">
        <h2>Login</h2>
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required>
<label for="password">Password:</label>
        <input type="password" id="password" name="password" required>
        <input type="submit" value="Login">
        
        Don't have an account? <a href="http://localhost:4200/FunnyBlog2.0/c1.4/2024/02/04/redirect.html">Sign up here</a>.
    </form>


</body>
<!-- 
Below JavaScript code is designed to handle user authentication in a web application. It's written to work with a backend server that uses JWT (JSON Web Tokens) for authentication.

The script defines a function when the page loads. This function is triggered when the Login button in the HTML form above is pressed. 
 -->
<script type="module">

    // uri variable and options object are obtained from config.js
    import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';

    function login_user(){
        // Set Authenticate endpoint
        const url = uri + '/api/users/authenticate';

        // Set the body of the request to include login data from the DOM
        const body = {
            // name: document.getElementById("name").value,
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
            // dob: document.getElementById("dob").value
        };

        // Change options according to Authentication requirements
        const authOptions = {
            ...options, // This will copy all properties from options
            method: 'POST', // Override the method property
            cache: 'no-cache', // Set the cache property
            body: JSON.stringify(body)
        };

        // Fetch JWT
        fetch(url, authOptions)
        .then(response => {
            // handle error response from Web API
            if (!response.ok) {
                if (response.status === 401) {
                    // Unauthorized - Redirect to 401 error page
                    window.location.href = "{{site.baseurl}}/401.html";
                }
                else if (response.status === 400) {
                    // Unauthorized - Redirect to 401 error page
                    window.location.href = "{{site.baseurl}}/400.html";
                }  
                else if (response.status === 403) {
                    // Forbidden - Redirect to 403 error page
                    window.location.href = "{{site.baseurl}}/403.html";
                } 
                else if (response.status === 404) {
                    // Not Found - Redirect to 404 error page
                    window.location.href = "{{site.baseurl}}/404.html";
                } 
                else {
                    // Handle other error responses
                    const errorMsg = 'Login error: ' + response.status;
                    console.log(errorMsg);
                }
                return;
            }
            // Success!!!
            // Redirect to the database page
            // window.location.href = "{{site.baseurl}}/AD_TimeBox.html";
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .then(data => {
            // Check if the user is an admin based on the role
            if (data && data.isAdmin == "yes") {
                console.log("User is an admin");
                window.location.href = "{{site.baseurl}}/database";
            } 
            else {
                console.log("User is not an admin");
                // Redirect to the database page
                window.location.href = "{{site.baseurl}}/AD_TimeBox.html";
            }
        })
        .catch(err => {
            console.error(err);
        });
    }
    // Attach login_user to the window object, allowing access to form action
    window.login_user = login_user;