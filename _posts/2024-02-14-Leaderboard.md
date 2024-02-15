<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #6e8efb, #a777e3);
    color: #333;
    padding: 20px;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.container {
    width: 90%;
    max-width: 600px;
    background: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}
h1 {
    text-align: center;
    color: #333;
    margin-bottom: 1.5rem;
}
.leaderboard {
    list-style: none;
}
.entry {
    background-color: #f7f7f7;
    border-left: 5px solid #5cb85c;
    margin: 10px 0;
    padding: 10px 15px;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: transform 0.2s ease-in-out;
}
.entry:hover {
    transform: translateY(-5px);
}
.entry:nth-child(odd) {
    background-color: #ffffff;
}
.entry:first-child {
    border-color: #ffda77;
}
.entry:first-child,
.entry:nth-child(2),
.entry:nth-child(3) {
    font-weight: bold;
}
/* Add a bit more flair */
.entry::before {
    content: counter(entry);
    counter-increment: entry;
    margin-right: 10px;
    background: #eee;
    border-radius: 50%;
    padding: 5px 10px;
    color: #333;
}
/* Responsive typography */
@media (max-width: 600px) {
    body {
        padding: 10px;
    }
.container {
        width: 100%;
    }
}</style>
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

