<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Obstacle Game</title>
<style>
    body {
        background-color: #87CEEB; /* Lighter sky blue */
        margin: 0;
        overflow: hidden;
    }
    canvas {
        display: block;
        margin: 0 auto;
        background-color: #ADD8E6; /* Light blue for a "daytime" feel */
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
        y: canvas.height / 2 - 15, // Adjusted for emoji
        width: 30,
        height: 30,
        speed: 5
    };

    const obstacleWidth = 40; // Adjusted for emoji
    const obstacleSpeed = 3;
    let obstacles = [];

    const coinSize = 20; // Adjusted for emoji
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
        obstacles.forEach(obstacle => {
            obstacle.x -= obstacleSpeed;
            if (obstacle.x + obstacleWidth < 0) {
                obstacles.shift();
            }
            if (character.x < obstacle.x + obstacleWidth &&
                character.x + character.width > obstacle.x &&
                character.y < obstacle.y + obstacleWidth &&
                character.y + character.height > obstacle.y) {
                endGame();
            }
        });

        coins.forEach(coin => {
            coin.x -= obstacleSpeed;
            if (coin.x + coinSize < 0) {
                coins.shift();
            }
            if (character.x < coin.x + coinSize &&
                character.x + character.width > coin.x &&
                character.y < coin.y + coinSize &&
                character.y + character.height > coin.y) {
                coins.shift();
                score++;
            }
        });

        if (Math.random() < 0.02) {
            obstacles.push({ x: canvas.width, y: Math.random() * (canvas.height - obstacleWidth) });
        }
        if (Math.random() < 0.01) {
            coins.push({ x: canvas.width, y: Math.random() * (canvas.height - coinSize) });
        }
    }

    function render() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        // Draw character as car emoji
        ctx.font = '30px Arial';
        ctx.fillText('🛸', character.x, character.y + character.height);

        // Draw obstacles as rock emojis
        obstacles.forEach(obstacle => {
            ctx.fillText('🪨', obstacle.x, obstacle.y + obstacleWidth);
        });

        // Draw coins as money bag emojis for a yellowish color
        coins.forEach(coin => {
            ctx.fillText('💰', coin.x, coin.y + coinSize);
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

    gameLoopInterval = setInterval(() => {
        update();
        render();
    }, 1000 / 60); // 60 frames per second
</script>
</body>
</html>
