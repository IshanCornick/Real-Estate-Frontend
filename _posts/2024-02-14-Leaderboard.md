<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Leaderboard</title>
<style>
    body {
        font-family: 'Arial', sans-serif;
        background-color: #f0f0f0;
        color: #333;
        margin: 0;
        padding: 20px;
        box-sizing: border-box;
    }
    .container {
        max-width: 600px;
        margin: auto;
        background: white;
        padding: 20px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
    }
     h1 {
        color: #333;
    }
     .leaderboard {
        list-style: none;
        padding: 0;
    }
     .entry {
        background-color: #efefef;
        border: 1px solid #ddd;
        margin-top: 10px;
        padding: 10px 15px;
        border-radius: 5px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
     .entry:nth-child(odd) {
        background-color: #f9f9f9;
    }
    .entry:first-child {
        background-color: #ffd700;
        color: #ffffff;
    }
     .entry:first-child,
    .entry:nth-child(2),
    .entry:nth-child(3) {
        font-weight: bold;
    }
    </style>
    <html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css"> <!-- Link to your CSS file -->
</head>
<body>
    <div class="container">
        <h1>Game Leaderboard</h1>
        <div id="leaderboard" class="leaderboard">
            <!-- Leaderboard entries will be added here by JavaScript -->
        </div>
    </div>
    <script src="script.js"></script> <!-- Link to your JavaScript file -->
</body>
</html>

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const results = [
            {player: "Alice", score: 10},
            {player: "Bob", score: 15},
            {player: "Charlie", score: 8},
            {player: "Diana", score: 12}
        ];
    
        const leaderboardDiv = document.getElementById('leaderboard');
        results.sort((a, b) => b.score - a.score); // Sort results by score
    
        results.forEach((result, index) => {
            const entryDiv = document.createElement('div');
            entryDiv.className = 'entry';
            entryDiv.textContent = `${index + 1}. ${result.player} - ${result.score}`;
            leaderboardDiv.appendChild(entryDiv);
        });
    });

