
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
        <button type="button" onclick="submitQuiz()">Submit Answers</button>
    </form>
    <div id="result"></div>

<script>
        function submitQuiz() {
            var score = 0;
            var totalQuestions = 2; // Update this based on the number of questions
            if(document.getElementById('q1b').checked) score++;
            if(document.getElementById('q2a').checked) score++;
            // Add more checks for additional questions
            
            var resultText = "";
            if(score === totalQuestions) {
                resultText = "You know your made you are in 10th grade or higher";
            } else if(score >= totalQuestions / 2) {
                resultText = "You missed some questions you are around 8th grade";
            } else {
                resultText = "You missed a lot of questions you are not great at math or around 6th grade";
            }

            document.getElementById('result').innerHTML = `<p>Your Score: ${score}/${totalQuestions}<br>${resultText}</p>`;
        }
    </script>
</body>
</html>
