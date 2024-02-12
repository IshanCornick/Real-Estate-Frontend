<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cookie Clicker</title>
  <style>
    body {
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
      background-color: #f0f0f0;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
    }
    #cookie {
      max-width: 100%;
      height: auto;
      border-radius: 50%;
      cursor: pointer;
      margin-bottom: 20px;
      transition: transform 0.2s;
    }
    #cookie:hover {
      transform: scale(1.1);
    }
    .shop, .minigames {
      background-color: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      max-width: 400px;
      width: 100%;
      margin-bottom: 20px;
    }
    .shop h2, .minigames h2 {
      margin-top: 0;
    }
    .shop-item {
      margin: 20px 0;
      border-top: 1px solid #ddd;
      padding-top: 20px;
    }
    .shop-item p,
    .shop-item button {
      margin: 5px 0;
      color: black; /* Text color set to black */
    }
    .shop-item button {
      padding: 10px 20px;
      background-color: #4CAF50;
      color: black;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .shop-item button:hover {
      background-color: #45a049;
    }
    .shop-item button:disabled {
      background-color: #ddd;
      cursor: not-allowed;
    }
  </style>
</head>
<body>
  <h1>Cookie Clicker</h1>
  <p>Click the cookie to earn points!</p>
  <img id="cookie" src="https://avatars.githubusercontent.com/u/54686997?v=4" alt="Cookie Image">
  <p>Points: <span id="points">0</span></p>

  <div class="shop">
    <h2>Shop</h2>
    <div class="shop-item">
      <p>Upgrade Click Power (+1 per click) - Cost: <span id="upgradeClickCost">25</span> points - Purchased: <span id="upgradeClickCount">0</span></p>
      <button id="upgradeClick">Buy</button>
    </div>
    <div class="shop-item">
      <p>Auto Click (1 click per second) - Cost: <span id="autoClickCost">100</span> points - Purchased: <span id="autoClickCount">0</span></p>
      <button id="autoClick">Buy</button>
    </div>
    <div class="shop-item">
      <p>Double Click Power (2x per click) - Cost: <span id="doubleClickCost">500</span> points - Purchased: <span id="doubleClickCount">0</span></p>
      <button id="doubleClick">Buy</button>
    </div>
    <div class="shop-item">
      <p>Auto Double Click (2 clicks per second) - Cost: <span id="autoDoubleClickCost">1000</span> points - Purchased: <span id="autoDoubleClickCount">0</span></p>
      <button id="autoDoubleClick">Buy</button>
    </div>
  </div>

  <div class="minigames">
    <h2>Mini Games</h2>
    <p>Guess the number between 1 and 2:</p>
    <input type="number" id="guessInput" min="1" max="2">
    <p>Enter the amount of points you want to pay to play:</p>
    <input type="number" id="gameCostInput" min="1">
    <button onclick="playGuessingGame()">Play</button>
    <p id="guessResult"></p>
  </div>

  <script>
    let points = 0;
    let clickPower = 1;
    let autoClickEnabled = false;
    let autoClickInterval;
    let upgradeClickCount = 0;
    let autoClickCount = 0;
    let doubleClickCount = 0;
    let autoDoubleClickCount = 0;
    let upgradeClickCost = 25;
    let autoClickCost = 100;
    let doubleClickCost = 500;
    let autoDoubleClickCost = 1000;

    const pointsDisplay = document.getElementById('points');
    const upgradeClickCostDisplay = document.getElementById('upgradeClickCost');
    const autoClickCostDisplay = document.getElementById('autoClickCost');
    const doubleClickCostDisplay = document.getElementById('doubleClickCost');
    const autoDoubleClickCostDisplay = document.getElementById('autoDoubleClickCost');
    const upgradeClickCountDisplay = document.getElementById('upgradeClickCount');
    const autoClickCountDisplay = document.getElementById('autoClickCount');
    const doubleClickCountDisplay = document.getElementById('doubleClickCount');
    const autoDoubleClickCountDisplay = document.getElementById('autoDoubleClickCount');
    const cookie = document.getElementById('cookie');
    const upgradeClickButton = document.getElementById('upgradeClick');
    const autoClickButton = document.getElementById('autoClick');
    const doubleClickButton = document.getElementById('doubleClick');
    const autoDoubleClickButton = document.getElementById('autoDoubleClick');

    cookie.addEventListener('click', () => {
      points += clickPower;
      updatePointsDisplay();
    });

    upgradeClickButton.addEventListener('click', () => {
      if (points >= upgradeClickCost) {
        points -= upgradeClickCost;
        clickPower++;
        upgradeClickCount++;
        upgradeClickCost = Math.floor(10 * Math.pow(1.1, upgradeClickCount)); // Exponential increase in cost
        updateShopDisplay();
        updatePointsDisplay();
      } else {
        alert('Not enough points!');
      }
    });

    autoClickButton.addEventListener('click', () => {
      if (points >= autoClickCost && !autoClickEnabled) {
        points -= autoClickCost;
        autoClickEnabled = true;
        autoClickInterval = setInterval(() => {
          points += clickPower;
          updatePointsDisplay();
        }, 1000);
        autoClickCount++;
        autoClickCost = Math.floor(50 * Math.pow(1.1, autoClickCount)); // Exponential increase in cost
        autoClickButton.disabled = true;
        updateShopDisplay();
        updatePointsDisplay();
      } else if (autoClickEnabled) {
        alert('Auto Click already enabled!');
      } else {
        alert('Not enough points!');
      }
    });

    doubleClickButton.addEventListener('click', () => {
      if (points >= doubleClickCost) {
        points -= doubleClickCost;
        clickPower *= 2;
        doubleClickCount++;
        doubleClickCost = Math.floor(100 * Math.pow(1.1, doubleClickCount)); // Exponential increase in cost
        updateShopDisplay();
        updatePointsDisplay();
      } else {
        alert('Not enough points!');
      }
    });

    autoDoubleClickButton.addEventListener('click', () => {
      if (points >= autoDoubleClickCost && !autoClickEnabled) {
        points -= autoDoubleClickCost;
        autoClickEnabled = true;
        autoClickInterval = setInterval(() => {
          points += clickPower * 2;
          updatePointsDisplay();
        }, 500); // Execute every 0.5 seconds for double click
        autoDoubleClickCount++;
        autoDoubleClickCost = Math.floor(200000 * Math.pow(1.1, autoDoubleClickCount)); // Exponential increase in cost
        autoDoubleClickButton.disabled = true;
        updateShopDisplay();
        updatePointsDisplay();
      } else if (autoClickEnabled) {
        alert('Auto Double Click already enabled!');
      } else {
        alert('Not enough points!');
      }
    });

    function updatePointsDisplay() {
      pointsDisplay.textContent = points;
      if (points >= 200) {
        miniGamesSection.style.display = 'block'; // Display the mini-games section when the player has at least 200 points
      }
    }

    function updateShopDisplay() {
      upgradeClickCostDisplay.textContent = upgradeClickCost;
      autoClickCostDisplay.textContent = autoClickCost;
      doubleClickCostDisplay.textContent = doubleClickCost;
      autoDoubleClickCostDisplay.textContent = autoDoubleClickCost;
      upgradeClickCountDisplay.textContent = upgradeClickCount;
      autoClickCountDisplay.textContent = autoClickCount;
      doubleClickCountDisplay.textContent = doubleClickCount;
      autoDoubleClickCountDisplay.textContent = autoDoubleClickCount;
    }

    function playGuessingGame() {
      const guessInput = document.getElementById('guessInput');
      const gameCostInput = document.getElementById('gameCostInput');
      const guessResult = document.getElementById('guessResult');

      // Check if the player has enough points to play the game
      if (points >= gameCostInput.value) {
        points -= gameCostInput.value; // Deduct the chosen points for playing the game

        const randomNumber = Math.floor(Math.random() * 2) + 1; // Generate a random number between 1 and 2

        if (parseInt(guessInput.value) === randomNumber) {
          points += parseInt(gameCostInput.value) * 2; // Double the points if the guess is correct
          guessResult.textContent = 'Congratulations! You won and doubled your points!';
        } else {
          guessResult.textContent = 'Sorry, try again!';
        }
        
        updatePointsDisplay(); // Update the points display after playing the game
      } else {
        guessResult.textContent = 'Not enough points to play the game!';
      }
    }
  </script>
</body>
</html>