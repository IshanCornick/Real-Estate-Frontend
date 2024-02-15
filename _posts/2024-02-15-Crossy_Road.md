<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Crossy R</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(#87CEEB, #ffffff); /* Sky to ground gradient */
            font-family: 'Arial', sans-serif;
        }
        #gameCanvas {
            border: 3px solid #333;
            margin-top: 10px;
        }
        #gameOver {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 3em;
            color: white;
            text-shadow: 2px 2px #000;
            background: rgba(0, 0, 0, 0.75);
            padding: 20px;
            border-radius: 10px;
        }
    </style>
</head>
<body>
    <div id="score-container">Score: <span id="score">0</span></div>
    <canvas id="gameCanvas" width="600" height="400"></canvas>
    <div id="gameOver">Game Over</div>

 <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreDisplay = document.getElementById('score');
        const gameOverDisplay = document.getElementById('gameOver');
        let score = 0;
        let gameRunning = true;

        let player = {
            x: canvas.width / 2,
            y: canvas.height - 30,
            width: 20,
            height: 20,
            color: '#FF4500',
            move: 20
        };

        let obstacles = [
            // Start with two obstacles
            { x: -100, y: 100, width: 80, height: 20, color: '#000', speed: 2 },
            { x: canvas.width + 100, y: 200, width: 80, height: 20, color: '#000', speed: -3 },
            // Add more obstacles here
        ];

        let pointsObject = {
            x: Math.random() * (canvas.width - 20),
            y: Math.random() * (canvas.height - 20),
            width: 10,
            height: 10,
            color: '#FFFF00'
        };

        function drawPlayer() {
            ctx.fillStyle = player.color;
            ctx.fillRect(player.x, player.y, player.width, player.height);
        }

        function drawObstacles() {
            obstacles.forEach(obstacle => {
                ctx.fillStyle = obstacle.color;
                ctx.fillRect(obstacle.x, obstacle.y, obstacle.width, obstacle.height);
                // Move the obstacle and check for off-screen
                obstacle.x += obstacle.speed;
                if (obstacle.x < -100 || obstacle.x > canvas.width) {
                    obstacle.x = obstacle.speed < 0 ? canvas.width + 100 : -100;
                }
            });
        }

        function drawPoints() {
            ctx.fillStyle = pointsObject.color;
            ctx.fillRect(pointsObject.x, pointsObject.y, pointsObject.width, pointsObject.height);
        }

        function detectCollision(obstacles, player) {
            return obstacles.some(obstacle => {
                return (
                    player.x < obstacle.x + obstacle.width &&
                    player.x + player.width > obstacle.x &&
                    player.y < obstacle.y + obstacle.height &&
                    player.y + player.height > obstacle.y
                );
            });
        }

        function detectPointCollection(player, pointsObject) {
            if (
                player.x < pointsObject.x + pointsObject.width &&
                player.x + player.width > pointsObject.x &&
                player.y < pointsObject.y + pointsObject.height &&
                player.y + player.height > pointsObject.y
            ) {
                // Reset points object location
                pointsObject.x = Math.random() * (canvas.width - 20);
                pointsObject.y = Math.random() * (canvas.height - 20);
                score += 10; // Increase score
                scoreDisplay.textContent = score; // Update score display
            }
        }

        function gameOver() {
            gameRunning = false;
            gameOverDisplay.style.display = 'block';
        }

        function gameLoop() {
            if (!gameRunning) return;
            ctx.clearRect(0, 0, canvas.width, canvas.height); // Clear canvas
            drawPlayer();
            drawObstacles();
            drawPoints();
            detectPointCollection(player
