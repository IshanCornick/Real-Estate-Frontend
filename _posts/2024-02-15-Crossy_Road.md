<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Simple Crossy Road-like Game</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #87CEEB;
        }
        canvas {
            border: 1px solid #000;
            background-color: #8FBC8F;
        }
    </style>
</head>
<body>
    <div>Score: <span id="score">0</span></div>
    <canvas id="gameCanvas" width="600" height="600"></canvas>

<script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreDisplay = document.getElementById('score');
        let score = 0;

        let player = {
            x: canvas.width / 2,
            y: canvas.height - 30,
            width: 20,
            height: 20,
            color: '#FF4500',
            move: 20
        };

        let obstacles = [
            { x: 100, y: 100, width: 100, height: 20, color: '#000' },
            { x: 300, y: 200, width: 100, height: 20, color: '#000' },
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

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height); // Clear canvas
            drawPlayer();
            drawObstacles();
            drawPoints();
            detectPointCollection(player, pointsObject);
        }

        setInterval(gameLoop, 50); // Game loop runs every 50ms

        document.addEventListener('keydown', function(event) {
            if (event.key === 'ArrowUp') player.y -= player.move;
            if (event.key === 'ArrowDown') player.y += player.move;
            if (event.key === 'ArrowLeft') player.x -= player.move;
            if (event.key === 'ArrowRight') player.x += player.move;

            // Check for collision with any of the obstacles
            if (detectCollision(obstacles, player)) {
                console.log("Collision detected!");
                // Handle collision (e.g., end game, lose a life, etc.)
            }
        });
    </script>
</body>
</html>
