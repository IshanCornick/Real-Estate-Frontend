<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Obstacle Game</title>
<style>
    body {
        background-color: #f0f0f0;
        margin: 0;
        overflow: hidden;
    }
    canvas {
        display: block;
        margin: 0 auto;
        background-color: #fff;
        border: 2px solid #000;
    }
    #endScreen {
        display: none;
        position: absolute;
        width: 100%;
        height: 100vh;
        top: 0;
        left: 0;
        background-color: rgba(0, 0, 0, 0.5);
        text-align: center;
        padding-top: 200px;
        font-size: 36px;
        color: white;
    }
</style>
</head>
<body>
<canvas id="gameCanvas" width="800" height="400"></canvas>
<div id="endScreen">
    <div>Game Over!</div>
    <div id="finalScore"></div>
    <button onclick="restartGame()">Restart</button>
</div>
<script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');

    const character = {
        x: 50,
        y: canvas.height / 2,
        width: 30,
        height: 30,
        speed: 5
    };

    const obstacleWidth = 20;
    const obstacleSpeed = 3;
    let obstacles = [];

    const coinSize = 10;
    let coins = [];

    let score = 0;
    let gameLoopInterval;

    window.addEventListener('keydown', function(event) {
        if (event.key === 'ArrowUp' && character.y > 0) {
            character.y -= character.speed;
        } else if (event.key === 'ArrowDown' && character.y < canvas.height - character.height) {
            character.y += character.speed;
        }
    });

    function update() {
        // Move obstacles
        obstacles.forEach(obstacle => {
            obstacle.x -= obstacleSpeed;
            if (obstacle.x + obstacleWidth < 0) {
                obstacles.shift();
            }
            // Check collision with character
            if (character.x < obstacle.x + obstacleWidth &&
                character.x + character.width > obstacle.x &&
                character.y < obstacle.y + obstacleWidth &&
                character.y + character.height > obstacle.y) {
                endGame();
            }
        });

        // Move coins
        coins.forEach(coin => {
            coin.x -= obstacleSpeed;
            if (coin.x + coinSize < 0) {
                coins.shift();
            }
            // Check collision with character
            if (character.x < coin.x + coinSize &&
                character.x + character.width > coin.x &&
                character.y < coin.y + coinSize &&
                character.y + character.height > coin.y) {
                coins.shift();
                score++;
            }
        });

        // Add new obstacles and coins
        if (Math.random() < 0.02) {
            obstacles.push({ x: canvas.width, y: Math.random() * (canvas.height - obstacleWidth) });
        }
        if (Math.random() < 0.01) {
            coins.push({ x: canvas.width, y: Math.random() * (canvas.height - coinSize) });
        }
    }

    function render() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        // Draw character
        ctx.fillStyle = '#ff0000';
        ctx.fillRect(character.x, character.y, character.width, character.height);

        // Draw obstacles
        ctx.fillStyle = '#000000';
        obstacles.forEach(obstacle => {
            ctx.fillRect(obstacle.x, obstacle.y, obstacleWidth, obstacleWidth);
        });

        // Draw coins
        ctx.fillStyle = '#ffd700';
        coins.forEach(coin => {
            ctx.fillRect(coin.x, coin.y, coinSize, coinSize);
        });

        // Draw score
        ctx.fillStyle = '#000000';
        ctx.font = '20px Arial';
        ctx.fillText('Score: ' + score, 10, 25);
    }

    function endGame() {
        clearInterval(gameLoopInterval);
        document.getElementById('finalScore').innerText = 'Final Score: ' + score;
        document.getElementById('endScreen').style.display = 'block';
    }

    function restartGame() {
        document.location.reload();
    }

    // Start the game loop
    gameLoopInterval = setInterval(() => {
        update();
        render();
    }, 1000 / 60); // 60 frames per second
</script>
</body>
</html>
