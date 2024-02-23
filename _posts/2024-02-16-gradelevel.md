
<html>
<head>
    <title>Math Level Quiz</title>
    <style>
        .question {
            margin-bottom: 20px;
        }
    </style>
</head>
<body>
    <h2>Math Level Quiz</h2>
    <form id="mathQuiz">
        <div class="question">
            <p>1. What is 7 + 8?</p>
            <input type="radio" id="q1a" name="q1" value="A"><label for="q1a">A) 13</label><br>
            <input type="radio" id="q1b" name="q1" value="B"><label for="q1b">B) 15</label><br>
            <input type="radio" id="q1c" name="q1" value="C"><label for="q1c">C) 16</label><br>
            <input type="radio" id="q1d" name="q1" value="D"><label for="q1d">D) 14</label>
        </div>
        <div class="question">
            <p>2. What is 45 divided by 9?</p>
            <input type="radio" id="q2a" name="q2" value="A"><label for="q2a">A) 5</label><br>
            <input type="radio" id="q2b" name="q2" value="B"><label for="q2b">B) 6</label><br>
            <input type="radio" id="q2c" name="q2" value="C"><label for="q2c">C) 7</label><br>
            <input type="radio" id="q2d" name="q2" value="D"><label for="q2d">D) 4</label>
        </div>
        <!-- Add more questions as needed -->
        
 </form>
<div id="result"></div>

<button type="button" onclick="submitQuiz()">Submit Answers</button>
    <div id="result"></div>
    <div id="quizResultsDisplay">
    </div>

<script>
    function submitQuiz() {
    var score = 0;
    var totalQuestions = 2; // Adjust based on your quiz's total questions
    var quizResults = {
        correctAnswers: 0,
        totalQuestions: totalQuestions,
        gradeLevel: "",
    };

    // Checking answers (example)
    if(document.getElementById('q1b').checked) score++;
    if(document.getElementById('q2a').checked) score++;

    // Updating quizResults object
    quizResults.correctAnswers = score;

    // Determine the grade level based on score
    if(score === totalQuestions) {
        quizResults.gradeLevel = "10th grade or higher";
    } else if(score >= totalQuestions / 2) {
        quizResults.gradeLevel = "around 8th grade";
    } else {
        quizResults.gradeLevel = "around 6th grade";
    }

    // Display results on the webpage
    // Ensure you have an element with ID 'quizResultsDisplay' in your HTML
    document.getElementById('quizResultsDisplay').textContent = `Quiz Results: ${JSON.stringify(quizResults)}`;



    // Prepare to send the results to the API
    const url ='http://127.0.0.1:8086/api/users/diet';
    const body = { quizResults: quizResults };
    const authOptions = {
        mode: 'cors',
        credentials: 'include',
        headers: {
            'Content-Type': 'application/json',
        },
        method: 'PUT',
        cache: 'no-cache',
        body: JSON.stringify(body)
    };

    // Send the quiz results to the API
    fetch(url, authOptions)
    .then(response => {
        if (!response.ok) {
            // Handle error response from the Web API
            console.error('Error: ' + response.status);
            return;
        }
        // Success handling here
        // For example, display a success message or redirect
    })
    .catch(err => {
        // Handle potential errors, such as network issues
        console.error(err);
    });
}

</script>


