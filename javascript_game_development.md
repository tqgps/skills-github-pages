# JavaScript Game Development Tutorial

## Table of Contents
1. [Game Development Basics](#basics)
2. [Setting Up Your First Game](#setup)
3. [Game 1: Number Guessing Game](#game1)
4. [Game 2: Snake Game](#game2)
5. [Game 3: Pong Game](#game3)
6. [Game Development Concepts](#concepts)
7. [Advanced Techniques](#advanced)
8. [Game Libraries and Frameworks](#libraries)
9. [Publishing Your Games](#publishing)

---

## Game Development Basics {#basics}

### What Makes a Game?
- **Game Loop**: Continuous cycle of update and render
- **Player Input**: Keyboard, mouse, touch interactions
- **Game State**: Current condition of the game (menu, playing, game over)
- **Graphics**: Visual representation of game elements
- **Sound**: Audio feedback and music
- **Physics**: Movement, collision detection, gravity

### Technologies for JavaScript Games
1. **HTML5 Canvas**: 2D graphics and animations
2. **WebGL**: 3D graphics and advanced 2D
3. **CSS3**: Simple animations and styling
4. **Web Audio API**: Sound and music
5. **Game Libraries**: Phaser, Three.js, PixiJS

---

## Setting Up Your First Game {#setup}

Let's start with a basic HTML template for game development:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My JavaScript Game</title>
    <style>
        body {
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: #222;
            font-family: Arial, sans-serif;
        }
        
        canvas {
            border: 2px solid #fff;
            background: #000;
        }
        
        .game-container {
            text-align: center;
            color: white;
        }
        
        .controls {
            margin-top: 20px;
            color: #ccc;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>JavaScript Game</h1>
        <canvas id="gameCanvas" width="800" height="600"></canvas>
        <div class="controls">
            <p>Use arrow keys to move</p>
        </div>
    </div>
    
    <script>
        // Game code goes here
    </script>
</body>
</html>
```

---

## Game 1: Number Guessing Game {#game1}

Let's start with a simple text-based game to understand game logic:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Number Guessing Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            text-align: center;
        }
        
        .game-container {
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
        }
        
        input, button {
            padding: 15px;
            margin: 10px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
        }
        
        button {
            background: #4CAF50;
            color: white;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #45a049;
        }
        
        .message {
            margin: 20px 0;
            padding: 15px;
            border-radius: 8px;
            font-weight: bold;
        }
        
        .success { background: rgba(76, 175, 80, 0.3); }
        .error { background: rgba(244, 67, 54, 0.3); }
        .info { background: rgba(33, 150, 243, 0.3); }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        
        .stat {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 8px;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>🎯 Number Guessing Game</h1>
        <p>I'm thinking of a number between 1 and 100!</p>
        
        <div class="stats">
            <div class="stat">
                <div>Attempts</div>
                <div id="attempts">0</div>
            </div>
            <div class="stat">
                <div>Best Score</div>
                <div id="bestScore">-</div>
            </div>
            <div class="stat">
                <div>Games Won</div>
                <div id="gamesWon">0</div>
            </div>
        </div>
        
        <div>
            <input type="number" id="guessInput" placeholder="Enter your guess" min="1" max="100">
            <button onclick="makeGuess()">Guess!</button>
            <button onclick="newGame()">New Game</button>
        </div>
        
        <div id="message" class="message info">Make your first guess!</div>
        <div id="guessHistory"></div>
    </div>

    <script>
        class NumberGuessingGame {
            constructor() {
                this.secretNumber = 0;
                this.attempts = 0;
                this.maxAttempts = 10;
                this.guessHistory = [];
                this.gamesWon = parseInt(localStorage.getItem('gamesWon')) || 0;
                this.bestScore = parseInt(localStorage.getItem('bestScore')) || null;
                
                this.updateDisplay();
                this.newGame();
            }
            
            newGame() {
                this.secretNumber = Math.floor(Math.random() * 100) + 1;
                this.attempts = 0;
                this.guessHistory = [];
                
                document.getElementById('guessInput').value = '';
                document.getElementById('guessInput').disabled = false;
                this.showMessage('I\'ve picked a new number! Make your guess.', 'info');
                this.updateDisplay();
                this.updateHistory();
            }
            
            makeGuess() {
                const input = document.getElementById('guessInput');
                const guess = parseInt(input.value);
                
                if (isNaN(guess) || guess < 1 || guess > 100) {
                    this.showMessage('Please enter a number between 1 and 100!', 'error');
                    return;
                }
                
                this.attempts++;
                this.guessHistory.push(guess);
                
                if (guess === this.secretNumber) {
                    this.winGame();
                } else if (this.attempts >= this.maxAttempts) {
                    this.loseGame();
                } else {
                    const hint = guess < this.secretNumber ? 'Too low! 📈' : 'Too high! 📉';
                    const remaining = this.maxAttempts - this.attempts;
                    this.showMessage(`${hint} You have ${remaining} attempts left.`, 'info');
                }
                
                input.value = '';
                this.updateDisplay();
                this.updateHistory();
            }
            
            winGame() {
                this.gamesWon++;
                localStorage.setItem('gamesWon', this.gamesWon);
                
                if (!this.bestScore || this.attempts < this.bestScore) {
                    this.bestScore = this.attempts;
                    localStorage.setItem('bestScore', this.bestScore);
                }
                
                document.getElementById('guessInput').disabled = true;
                this.showMessage(`🎉 Congratulations! You found ${this.secretNumber} in ${this.attempts} attempts!`, 'success');
                this.updateDisplay();
            }
            
            loseGame() {
                document.getElementById('guessInput').disabled = true;
                this.showMessage(`💔 Game Over! The number was ${this.secretNumber}. Better luck next time!`, 'error');
            }
            
            showMessage(text, type) {
                const messageEl = document.getElementById('message');
                messageEl.textContent = text;
                messageEl.className = `message ${type}`;
            }
            
            updateDisplay() {
                document.getElementById('attempts').textContent = this.attempts;
                document.getElementById('gamesWon').textContent = this.gamesWon;
                document.getElementById('bestScore').textContent = this.bestScore || '-';
            }
            
            updateHistory() {
                const historyEl = document.getElementById('guessHistory');
                if (this.guessHistory.length > 0) {
                    historyEl.innerHTML = '<h3>Your Guesses:</h3>' + 
                        this.guessHistory.map(guess => `<span style="margin: 5px; padding: 5px 10px; background: rgba(255,255,255,0.2); border-radius: 5px; display: inline-block;">${guess}</span>`).join('');
                } else {
                    historyEl.innerHTML = '';
                }
            }
        }
        
        // Initialize game
        let game;
        
        function makeGuess() {
            game.makeGuess();
        }
        
        function newGame() {
            game.newGame();
        }
        
        // Start the game when page loads
        window.addEventListener('load', () => {
            game = new NumberGuessingGame();
            
            // Allow Enter key to make guess
            document.getElementById('guessInput').addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    makeGuess();
                }
            });
        });
    </script>
</body>
</html>
```

---

## Game 2: Snake Game {#game2}

Now let's create a classic Snake game using HTML5 Canvas:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        body {
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(45deg, #1e3c72, #2a5298);
            font-family: 'Arial', sans-serif;
        }
        
        .game-container {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 20px;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            color: #fff;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        canvas {
            border: 3px solid #fff;
            border-radius: 10px;
            background: #000;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
        }
        
        .controls {
            margin-top: 20px;
            color: #fff;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .score {
            font-size: 24px;
            font-weight: bold;
        }
        
        .instructions {
            font-size: 14px;
            opacity: 0.8;
        }
        
        button {
            padding: 10px 20px;
            margin: 0 10px;
            border: none;
            border-radius: 8px;
            background: #4CAF50;
            color: white;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #45a049;
        }
        
        .game-over {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.9);
            color: white;
            padding: 30px;
            border-radius: 15px;
            text-align: center;
            display: none;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>🐍 Snake Game</h1>
        <canvas id="gameCanvas" width="400" height="400"></canvas>
        <div class="controls">
            <div class="score">Score: <span id="score">0</span></div>
            <div>
                <button onclick="pauseGame()">Pause</button>
                <button onclick="resetGame()">Reset</button>
            </div>
            <div class="instructions">Use arrow keys or WASD</div>
        </div>
        
        <div id="gameOver" class="game-over">
            <h2>Game Over!</h2>
            <p>Final Score: <span id="finalScore">0</span></p>
            <button onclick="resetGame()">Play Again</button>
        </div>
    </div>

    <script>
        class SnakeGame {
            constructor() {
                this.canvas = document.getElementById('gameCanvas');
                this.ctx = this.canvas.getContext('2d');
                this.gridSize = 20;
                this.tileCount = this.canvas.width / this.gridSize;
                
                this.snake = [
                    {x: 10, y: 10}
                ];
                this.food = {};
                this.dx = 0;
                this.dy = 0;
                this.score = 0;
                this.gameRunning = false;
                this.gamePaused = false;
                
                this.generateFood();
                this.setupEventListeners();
                this.gameLoop();
            }
            
            setupEventListeners() {
                document.addEventListener('keydown', (e) => {
                    if (!this.gameRunning || this.gamePaused) return;
                    
                    switch(e.key) {
                        case 'ArrowUp':
                        case 'w':
                        case 'W':
                            if (this.dy !== 1) {
                                this.dx = 0;
                                this.dy = -1;
                            }
                            break;
                        case 'ArrowDown':
                        case 's':
                        case 'S':
                            if (this.dy !== -1) {
                                this.dx = 0;
                                this.dy = 1;
                            }
                            break;
                        case 'ArrowLeft':
                        case 'a':
                        case 'A':
                            if (this.dx !== 1) {
                                this.dx = -1;
                                this.dy = 0;
                            }
                            break;
                        case 'ArrowRight':
                        case 'd':
                        case 'D':
                            if (this.dx !== -1) {
                                this.dx = 1;
                                this.dy = 0;
                            }
                            break;
                        case ' ':
                            this.pauseGame();
                            break;
                    }
                });
                
                // Start game on first key press
                document.addEventListener('keydown', () => {
                    if (!this.gameRunning) {
                        this.startGame();
                    }
                }, { once: true });
            }
            
            startGame() {
                this.gameRunning = true;
                this.dx = 1;
                this.dy = 0;
            }
            
            pauseGame() {
                if (!this.gameRunning) return;
                this.gamePaused = !this.gamePaused;
            }
            
            resetGame() {
                this.snake = [{x: 10, y: 10}];
                this.dx = 0;
                this.dy = 0;
                this.score = 0;
                this.gameRunning = false;
                this.gamePaused = false;
                this.generateFood();
                this.updateScore();
                document.getElementById('gameOver').style.display = 'none';
            }
            
            generateFood() {
                do {
                    this.food = {
                        x: Math.floor(Math.random() * this.tileCount),
                        y: Math.floor(Math.random() * this.tileCount)
                    };
                } while (this.snake.some(segment => segment.x === this.food.x && segment.y === this.food.y));
            }
            
            update() {
                if (!this.gameRunning || this.gamePaused) return;
                
                const head = {x: this.snake[0].x + this.dx, y: this.snake[0].y + this.dy};
                
                // Check wall collision
                if (head.x < 0 || head.x >= this.tileCount || head.y < 0 || head.y >= this.tileCount) {
                    this.gameOver();
                    return;
                }
                
                // Check self collision
                if (this.snake.some(segment => segment.x === head.x && segment.y === head.y)) {
                    this.gameOver();
                    return;
                }
                
                this.snake.unshift(head);
                
                // Check food collision
                if (head.x === this.food.x && head.y === this.food.y) {
                    this.score += 10;
                    this.updateScore();
                    this.generateFood();
                } else {
                    this.snake.pop();
                }
            }
            
            draw() {
                // Clear canvas
                this.ctx.fillStyle = '#000';
                this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height);
                
                // Draw snake
                this.ctx.fillStyle = '#0f0';
                this.snake.forEach((segment, index) => {
                    if (index === 0) {
                        // Head
                        this.ctx.fillStyle = '#4f4';
                    } else {
                        this.ctx.fillStyle = '#0f0';
                    }
                    this.ctx.fillRect(
                        segment.x * this.gridSize + 2,
                        segment.y * this.gridSize + 2,
                        this.gridSize - 4,
                        this.gridSize - 4
                    );
                });
                
                // Draw food
                this.ctx.fillStyle = '#f00';
                this.ctx.beginPath();
                this.ctx.arc(
                    this.food.x * this.gridSize + this.gridSize / 2,
                    this.food.y * this.gridSize + this.gridSize / 2,
                    this.gridSize / 2 - 2,
                    0,
                    2 * Math.PI
                );
                this.ctx.fill();
                
                // Draw pause text
                if (this.gamePaused) {
                    this.ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
                    this.ctx.font = '30px Arial';
                    this.ctx.textAlign = 'center';
                    this.ctx.fillText('PAUSED', this.canvas.width / 2, this.canvas.height / 2);
                }
                
                // Draw start instruction
                if (!this.gameRunning) {
                    this.ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
                    this.ctx.font = '20px Arial';
                    this.ctx.textAlign = 'center';
                    this.ctx.fillText('Press any key to start!', this.canvas.width / 2, this.canvas.height / 2);
                }
            }
            
            updateScore() {
                document.getElementById('score').textContent = this.score;
            }
            
            gameOver() {
                this.gameRunning = false;
                document.getElementById('finalScore').textContent = this.score;
                document.getElementById('gameOver').style.display = 'block';
            }
            
            gameLoop() {
                this.update();
                this.draw();
                setTimeout(() => this.gameLoop(), 150);
            }
        }
        
        // Initialize game
        let game;
        
        function pauseGame() {
            if (game) game.pauseGame();
        }
        
        function resetGame() {
            if (game) game.resetGame();
        }
        
        window.addEventListener('load', () => {
            game = new SnakeGame();
        });
    </script>
</body>
</html>
```

---

## Game 3: Pong Game {#game3}

Let's create a classic Pong game with AI opponent:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pong Game</title>
    <style>
        body {
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            font-family: 'Arial', sans-serif;
        }
        
        .game-container {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 20px;
            backdrop-filter: blur(10px);
        }
        
        h1 {
            color: #fff;
            margin-bottom: 20px;
        }
        
        canvas {
            border: 3px solid #fff;
            border-radius: 10px;
            background: #000;
        }
        
        .controls {
            margin-top: 20px;
            color: #fff;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .score {
            font-size: 24px;
            font-weight: bold;
        }
        
        button {
            padding: 10px 20px;
            margin: 0 10px;
            border: none;
            border-radius: 8px;
            background: #4CAF50;
            color: white;
            cursor: pointer;
            font-size: 16px;
        }
        
        button:hover {
            background: #45a049;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>🏓 Pong Game</h1>
        <canvas id="gameCanvas" width="800" height="400"></canvas>
        <div class="controls">
            <div class="score">Player: <span id="playerScore">0</span></div>
            <div>
                <button onclick="game.togglePause()">Pause</button>
                <button onclick="game.reset()">Reset</button>
            </div>
            <div class="score">AI: <span id="aiScore">0</span></div>
        </div>
        <div style="color: white; margin-top: 10px;">
            Use W/S keys or mouse to move your paddle
        </div>
    </div>

    <script>
        class PongGame {
            constructor() {
                this.canvas = document.getElementById('gameCanvas');
                this.ctx = this.canvas.getContext('2d');
                
                // Game objects
                this.ball = {
                    x: this.canvas.width / 2,
                    y: this.canvas.height / 2,
                    dx: 5,
                    dy: 3,
                    radius: 10
                };
                
                this.playerPaddle = {
                    x: 20,
                    y: this.canvas.height / 2 - 50,
                    width: 15,
                    height: 100,
                    speed: 8
                };
                
                this.aiPaddle = {
                    x: this.canvas.width - 35,
                    y: this.canvas.height / 2 - 50,
                    width: 15,
                    height: 100,
                    speed: 6
                };
                
                // Game state
                this.playerScore = 0;
                this.aiScore = 0;
                this.gameRunning = true;
                this.gamePaused = false;
                
                // Input handling
                this.keys = {};
                this.mouseY = this.canvas.height / 2;
                
                this.setupEventListeners();
                this.gameLoop();
            }
            
            setupEventListeners() {
                // Keyboard controls
                document.addEventListener('keydown', (e) => {
                    this.keys[e.key.toLowerCase()] = true;
                    if (e.key === ' ') {
                        this.togglePause();
                        e.preventDefault();
                    }
                });
                
                document.addEventListener('keyup', (e) => {
                    this.keys[e.key.toLowerCase()] = false;
                });
                
                // Mouse controls
                this.canvas.addEventListener('mousemove', (e) => {
                    const rect = this.canvas.getBoundingClientRect();
                    this.mouseY = e.clientY - rect.top;
                });
            }
            
            update() {
                if (!this.gameRunning || this.gamePaused) return;
                
                // Update player paddle
                if (this.keys['w'] && this.playerPaddle.y > 0) {
                    this.playerPaddle.y -= this.playerPaddle.speed;
                }
                if (this.keys['s'] && this.playerPaddle.y < this.canvas.height - this.playerPaddle.height) {
                    this.playerPaddle.y += this.playerPaddle.speed;
                }
                
                // Mouse control for player paddle
                const targetY = this.mouseY - this.playerPaddle.height / 2;
                if (targetY >= 0 && targetY <= this.canvas.height - this.playerPaddle.height) {
                    this.playerPaddle.y = targetY;
                }
                
                // Update AI paddle (simple AI)
                const aiCenter = this.aiPaddle.y + this.aiPaddle.height / 2;
                const ballCenter = this.ball.y;
                
                if (aiCenter < ballCenter - 35) {
                    this.aiPaddle.y += this.aiPaddle.speed;
                } else if (aiCenter > ballCenter + 35) {
                    this.aiPaddle.y -= this.aiPaddle.speed;
                }
                
                // Keep AI paddle in bounds
                this.aiPaddle.y = Math.max(0, Math.min(this.canvas.height - this.aiPaddle.height, this.aiPaddle.y));
                
                // Update ball
                this.ball.x += this.ball.dx;
                this.ball.y += this.ball.dy;
                
                // Ball collision with top and bottom walls
                if (this.ball.y - this.ball.radius <= 0 || this.ball.y + this.ball.radius >= this.canvas.height) {
                    this.ball.dy = -this.ball.dy;
                }
                
                // Ball collision with player paddle
                if (this.ball.x - this.ball.radius <= this.playerPaddle.x + this.playerPaddle.width &&
                    this.ball.y >= this.playerPaddle.y &&
                    this.ball.y <= this.playerPaddle.y + this.playerPaddle.height &&
                    this.ball.dx < 0) {
                    
                    this.ball.dx = -this.ball.dx;
                    // Add some spin based on where the ball hits the paddle
                    const hitPos = (this.ball.y - this.playerPaddle.y) / this.playerPaddle.height;
                    this.ball.dy = (hitPos - 0.5) * 10;
                }
                
                // Ball collision with AI paddle
                if (this.ball.x + this.ball.radius >= this.aiPaddle.x &&
                    this.ball.y >= this.aiPaddle.y &&
                    this.ball.y <= this.aiPaddle.y + this.aiPaddle.height &&
                    this.ball.dx > 0) {
                    
                    this.ball.dx = -this.ball.dx;
                    const hitPos = (this.ball.y - this.aiPaddle.y) / this.aiPaddle.height;
                    this.ball.dy = (hitPos - 0.5) * 10;
                }
                
                // Ball goes off screen
                if (this.ball.x < 0) {
                    this.aiScore++;
                    this.resetBall();
                    this.updateScore();
                } else if (this.ball.x > this.canvas.width) {
                    this.playerScore++;
                    this.resetBall();
                    this.updateScore();
                }
            }
            
            draw() {
                // Clear canvas
                this.ctx.fillStyle = '#000';
                this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height);
                
                // Draw center line
                this.ctx.setLineDash([5, 15]);
                this.ctx.strokeStyle = '#fff';
                this.ctx.lineWidth = 3;
                this.ctx.beginPath();
                this.ctx.moveTo(this.canvas.width / 2, 0);
                this.ctx.lineTo(this.canvas.width / 2, this.canvas.height);
                this.ctx.stroke();
                this.ctx.setLineDash([]);
                
                // Draw paddles
                this.ctx.fillStyle = '#fff';
                this.ctx.fillRect(this.playerPaddle.x, this.playerPaddle.y, this.playerPaddle.width, this.playerPaddle.height);
                this.ctx.fillRect(this.aiPaddle.x, this.aiPaddle.y, this.aiPaddle.width, this.aiPaddle.height);
                
                // Draw ball
                this.ctx.beginPath();
                this.ctx.arc(this.ball.x, this.ball.y, this.ball.radius, 0, Math.PI * 2);
                this.ctx.fill();
                
                // Draw pause text
                if (this.gamePaused) {
                    this.ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
                    this.ctx.font = '40px Arial';
                    this.ctx.textAlign = 'center';
                    this.ctx.fillText('PAUSED', this.canvas.width / 2, this.canvas.height / 2);
                }
            }
            
            resetBall() {
                this.ball.x = this.canvas.width / 2;
                this.ball.y = this.canvas.height / 2;
                this.ball.dx = this.ball.dx > 0 ? -5 : 5; // Serve to opposite side
                this.ball.dy = (Math.random() - 0.5) * 6;
            }
            
            updateScore() {
                document.getElementById('playerScore').textContent = this.playerScore;
                document.getElementById('aiScore').textContent = this.aiScore;
            }
            
            togglePause() {
                this.gamePaused = !this.gamePaused;
            }
            
            reset() {
                this.playerScore = 0;
                this.aiScore = 0;
                this.resetBall();
                this.updateScore();
                this.gamePaused = false;
            }
            
            gameLoop() {
                this.update();
                this.draw();
                requestAnimationFrame(() => this.gameLoop());
            }
        }
        
        // Initialize game
        let game;
        
        window.addEventListener('load', () => {
            game = new PongGame();
        });
    </script>
</body>
</html>
```

---

## Game Development Concepts {#concepts}

### Game Loop
The heart of every game is the game loop:

```javascript
class GameLoop {
    constructor() {
        this.isRunning = false;
        this.lastTime = 0;
    }
    
    start() {
        this.isRunning = true;
        this.gameLoop(0);
    }
    
    stop() {
        this.isRunning = false;
    }
    
    gameLoop(currentTime) {
        if (!this.isRunning) return;
        
        const deltaTime = currentTime - this.lastTime;
        this.lastTime = currentTime;
        
        // Update game state
        this.update(deltaTime);
        
        // Render graphics
        this.render();
        
        // Schedule next frame
        requestAnimationFrame((time) => this.gameLoop(time));
    }
    
    update(deltaTime) {
        // Update game objects
        // Handle input
        // Check collisions
        // Update physics
    }
    
    render() {
        // Clear screen
        // Draw all game objects
        // Draw UI elements
    }
}
```

### Collision Detection
Basic collision detection for rectangles:

```javascript
function checkCollision(rect1, rect2) {
    return rect1.x < rect2.x + rect2.width &&
           rect1.x + rect1.width > rect2.x &&
           rect1.y < rect2.y + rect2.height &&
           rect1.y + rect1.height > rect2.y;
}

// Circle collision
function checkCircleCollision(circle1, circle2) {
    const dx = circle1.x - circle2.x;
    const dy = circle1.y - circle2.y;
    const distance = Math.sqrt(dx * dx + dy * dy);
    return distance < circle1.radius + circle2.radius;
}
```

### Input Handling
Robust input system:

```javascript
class InputHandler {
    constructor() {
        this.keys = {};
        this.mouse = { x: 0, y: 0, buttons: {} };
        
        this.setupEventListeners();
    }
    
    setupEventListeners() {
        document.addEventListener('keydown', (e) => {
            this.keys[e.code] = true;
        });
        
        document.addEventListener('keyup', (e) => {
            this.keys[e.code] = false;
        });
        
        document.addEventListener('mousemove', (e) => {
            this.mouse.x = e.clientX;
            this.mouse.y = e.clientY;
        });
        
        document.addEventListener('mousedown', (e) => {
            this.mouse.buttons[e.button] = true;
        });
        
        document.addEventListener('mouseup', (e) => {
            this.mouse.buttons[e.button] = false;
        });
    }
    
    isKeyPressed(keyCode) {
        return !!this.keys[keyCode];
    }
    
    isMouseButtonPressed(button) {
        return !!this.mouse.buttons[button];
    }
}
```

---

## Advanced Techniques {#advanced}

### Particle Systems
Create visual effects with particles:

```javascript
class Particle {
    constructor(x, y) {
        this.x = x;
        this.y = y;
        this.vx = (Math.random() - 0.5) * 10;
        this.vy = (Math.random() - 0.5) * 10;
        this.life = 60; // frames
        this.maxLife = 60;
    }
    
    update() {
        this.x += this.vx;
        this.y += this.vy;
        this.vy += 0.5; // gravity
        this.life--;
    }
    
    draw(ctx) {
        const alpha = this.life / this.maxLife;
        ctx.globalAlpha = alpha;
        ctx.fillStyle = `hsl(${60 - (1 - alpha) * 60}, 100%, 50%)`;
        ctx.beginPath();
        ctx.arc(this.x, this.y, 3, 0, Math.PI * 2);
        ctx.fill();
        ctx.globalAlpha = 1;
    }
    
    isDead() {
        return this.life <= 0;
    }
}

class ParticleSystem {
    constructor() {
        this.particles = [];
    }
    
    emit(x, y, count = 10) {
        for (let i = 0; i < count; i++) {
            this.particles.push(new Particle(x, y));
        }
    }
    
    update() {
        this.particles.forEach(particle => particle.update());
        this.particles = this.particles.filter(particle => !particle.isDead());
    }
    
    draw(ctx) {
        this.particles.forEach(particle => particle.draw(ctx));
    }
}
```

### Sound Integration
Add sounds to your games:

```javascript
class SoundManager {
    constructor() {
        this.sounds = {};
        this.audioContext = new (window.AudioContext || window.webkitAudioContext)();
    }
    
    async loadSound(name, url) {
        try {
            const response = await fetch(url);
            const arrayBuffer = await response.arrayBuffer();
            const audioBuffer = await this.audioContext.decodeAudioData(arrayBuffer);
            this.sounds[name] = audioBuffer;
        } catch (error) {
            console.error('Error loading sound:', error);
        }
    }
    
    playSound(name, volume = 1, pitch = 1) {
        if (!this.sounds[name]) return;
        
        const source = this.audioContext.createBufferSource();
        const gainNode = this.audioContext.createGain();
        
        source.buffer = this.sounds[name];
        source.playbackRate.value = pitch;
        gainNode.gain.value = volume;
        
        source.connect(gainNode);
        gainNode.connect(this.audioContext.destination);
        
        source.start();
    }
}
```

---

## Game Libraries and Frameworks {#libraries}

### Phaser.js
Popular 2D game framework:

```html
<script src="https://cdn.jsdelivr.net/npm/phaser@3.70.0/dist/phaser.min.js"></script>
<script>
class GameScene extends Phaser.Scene {
    constructor() {
        super({ key: 'GameScene' });
    }
    
    preload() {
        // Load assets
        this.load.image('player', 'player.png');
    }
    
    create() {
        // Create game objects
        this.player = this.add.sprite(400, 300, 'player');
        
        // Create input
        this.cursors = this.input.keyboard.createCursorKeys();
    }
    
    update() {
        // Game logic
        if (this.cursors.left.isDown) {
            this.player.x -= 5;
        }
        if (this.cursors.right.isDown) {
            this.player.x += 5;
        }
    }
}

const config = {
    type: Phaser.AUTO,
    width: 800,
    height: 600,
    scene: GameScene,
    physics: {
        default: 'arcade',
        arcade: {
            gravity: { y: 300 },
            debug: false
        }
    }
};

const game = new Phaser.Game(config);
</script>
```

### Three.js for 3D Games
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
// Basic 3D scene setup
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer();

renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// Create a cube
const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

camera.position.z = 5;

function animate() {
    requestAnimationFrame(animate);
    
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    
    renderer.render(scene, camera);
}

animate();
</script>
```

---

## Publishing Your Games {#publishing}

### GitHub Pages (Free)
1. Create a repository on GitHub
2. Upload your HTML file as `index.html`
3. Enable GitHub Pages in repository settings
4. Your game will be available at `username.github.io/repository-name`

### itch.io (Game Platform)
1. Create account at itch.io
2. Upload your HTML file and assets
3. Set as HTML5 game
4. Publish to itch.io community

### Optimization Tips
```javascript
// Use object pooling for frequently created/destroyed objects
class ObjectPool {
    constructor(createFn, resetFn, initialSize = 10) {
        this.createFn = createFn;
        this.resetFn = resetFn;
        this.pool = [];
        
        for (let i = 0; i < initialSize; i++) {
            this.pool.push(this.createFn());
        }
    }
    
    get() {
        if (this.pool.length > 0) {
            return this.pool.pop();
        }
        return this.createFn();
    }
    
    release(obj) {
        this.resetFn(obj);
        this.pool.push(obj);
    }
}

// Optimize canvas rendering
function optimizeCanvas(ctx) {
    // Use integer coordinates
    ctx.translate(0.5, 0.5);
    
    // Disable antialiasing for pixel art
    ctx.imageSmoothingEnabled = false;
    
    // Use efficient drawing methods
    ctx.fillRect(x | 0, y | 0, width | 0, height | 0);
}
```

## Next Steps

1. **Practice**: Build variations of these games
2. **Learn More**: Explore game design patterns
3. **Add Features**: Implement power-ups, levels, animations
4. **Join Community**: Share your games and get feedback
5. **Advanced Topics**: Learn about game engines, monetization, publishing

Happy game development! 🎮