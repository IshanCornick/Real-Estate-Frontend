<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .quiz-container {
            width: 90%;
            max-width: 600px;
            margin: auto;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .question {
            margin-bottom: 20px;
        }
        .question p {
            margin: 0;
            font-weight: bold;
        }
        button {
            cursor: pointer;
            background-color: #007BFF;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056B3;
        }
    </style>
</head>
<body>
   <div class="quiz-container">
    <h2>Quiz</h2>
    <form id="quizForm">
        <div class="question">
            <p>Question 1: What is 2 + 2?</p>
            <input type="text" name="question1" required>
        </div>
        <div class="question">
            <p>Question 2: What is the capital of France?</p>
            <input type="text" name="question2" required>
        </div>
        <div class="question">
            <p>Question 3: What is the derivative of x^2?</p>
            <input type="text" name="question3" required>
        </div>
        <div class="question">
            <p>Question 4: Who wrote 'To Kill a Mockingbird'?</p>
            <input type="text" name="question4" required>
        </div>
        <div class="question">
            <p>Question 5: What is the chemical symbol for gold?</p>
            <input type="text" name="question5" required>
        </div>
        <button type="submit">Submit</button>
    </form>
</div>
<script>
document.getElementById('quizForm').addEventListener('submit', function(e) {
    e.preventDefault();
    // Define correct answers
    const correctAnswers = {
        question1: '4',
        question2: 'Paris',
        question3: '2x',
        question4: 'Harper Lee',
        question5: 'Au',
    };
    // Collect form data
    const formData = new FormData(e.target);
    let score = 0;
    const quizResults = {};
    for (const [key, value] of formData.entries()) {
        quizResults[key] = value;
        if (value.trim().toLowerCase() === correctAnswers[key].toLowerCase()) {
            score++;
        }
    }
    // Log the user's answers
    console.log("User's Answers:", quizResults);
    // Determine the grade level based on score
    const totalQuestions = Object.keys(correctAnswers).length;
    const scorePercentage = (score / totalQuestions) * 100;
    let grade;
    if (scorePercentage >= 80) {
        grade = "High School";
    } else if (scorePercentage >= 50) {
        grade = "Middle School";
    } else {
        grade = "Elementary";
    }
    // Display grade level to the user
    alert(`Based on your quiz results, you are in: ${grade}`);
    // Example of sending quizResults to the backend (adjust as necessary for your backend)
    const url = 'http://127.0.0.1:8082/api/users/diet'; // Adjust URL as necessary
    const options = {
        method: 'PUT', // or 'POST' if creating new resource
        headers: {
            'Content-Type': 'application/json',
            // Include other headers as required, e.g., Authorization
        },
        body: JSON.stringify({ grade: grade }),
        mode: 'cors',
        credentials: 'include',
    };
    fetch(url, options)
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json(); // or .text() if expecting a text response
    })
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error('There has been a problem with your fetch operation:', error);
    });
});
</script>
</body>
</html>