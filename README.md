# Kannu
Kannugameworld.com
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kannu's Puzzle Game</title>
    <style>
        /* Main Styles */
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            overflow: hidden;
            color: white;
        }

        /* Neon Text Effect */
        .neon-text {
            text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #e60073, 0 0 40px #e60073;
            animation: neon-glow 1.5s ease-in-out infinite alternate;
        }
        @keyframes neon-glow {
            from { text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #e60073, 0 0 20px #e60073; }
            to { text-shadow: 0 0 10px #fff, 0 0 20px #ff4da6, 0 0 30px #ff4da6, 0 0 40px #ff4da6; }
        }

        /* Screens */
        .screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: rgba(0, 0, 0, 0.8);
            z-index: 10;
            text-align: center;
            transition: all 0.5s;
        }

        /* Mode Selection */
        .mode-select {
            display: flex;
            gap: 20px;
            margin: 30px 0;
            flex-wrap: wrap;
            justify-content: center;
        }
        .mode-btn {
            padding: 15px 25px;
            font-size: 18px;
            background: linear-gradient(45deg, #4e54c8, #8f94fb);
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        .mode-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.4);
        }

        /* Game Container */
        .game-container {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            transform: scale(0.9);
            transition: all 0.5s;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        /* Puzzle Board */
        .puzzle-board {
            display: grid;
            grid-gap: 8px;
            margin: 20px auto;
        }

        /* Tiles - Different Colors */
        .tile {
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            font-weight: bold;
            cursor: pointer;
            border-radius: 10px;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            color: white;
        }
        .tile:hover {
            transform: scale(1.05);
            opacity: 0.9;
        }

        /* Different sizes for different modes */
        .size-3 { grid-template-columns: repeat(3, 90px); }
        .size-4 { grid-template-columns: repeat(4, 80px); }
        .size-5 { grid-template-columns: repeat(5, 70px); }

        .size-3 .tile { width: 90px; height: 90px; font-size: 30px; }
        .size-4 .tile { width: 80px; height: 80px; font-size: 24px; }
        .size-5 .tile { width: 70px; height: 70px; font-size: 20px; }

        /* Tile Colors */
        .tile-1 { background: #FF6B6B; } /* Red */
        .tile-2 { background: #66A6FF; } /* Blue */
        .tile-3 { background: #FFB347; } /* Orange */
        .tile-4 { background: #A18CD1; } /* Purple */
        .tile-5 { background: #FF9FF3; } /* Pink */
        .tile-6 { background: #FDCB6E; } /* Yellow */
        .tile-7 { background: #55EFC4; } /* Green */
        .tile-8 { background: #FD79A8; } /* Dark Pink */
        .tile-9 { background: #74B9FF; } /* Light Blue */
        .tile-10 { background: #A29BFE; } /* Lavender */
        .tile-11 { background: #FF7675; } /* Coral */
        .tile-12 { background: #FAB1A0; } /* Peach */
        .tile-13 { background: #00CEC9; } /* Teal */
        .tile-14 { background: #E84393; } /* Pink Red */
        .tile-15 { background: #6C5CE7; } /* Purple Blue */

        .empty {
            background: rgba(255, 255, 255, 0.1);
            visibility: hidden;
        }

        /* Game Controls */
        .game-controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }
        .control-btn {
            padding: 10px 20px;
            font-size: 16px;
            background: linear-gradient(45deg, #4ecdc4, #66a6ff);
            color: white;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .control-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        /* Moves Counter */
        #moves {
            font-size: 18px;
            margin-top: 15px;
            color: #ddd;
        }
        .move-limit {
            color: #ff6b6b;
            font-weight: bold;
        }

        /* Share Button */
        .share-btn {
            position: fixed;
            bottom: 20px;
            left: 20px;
            padding: 10px 20px;
            background: linear-gradient(45deg, #4e54c8, #8f94fb);
            color: white;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .share-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        /* Hidden Class */
        .hidden {
            display: none !important;
        }

        /* Signature */
        .signature {
            position: fixed;
            bottom: 20px;
            right: 20px;
            font-size: 14px;
            color: rgba(255, 255, 255, 0.7);
            text-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
        }

        /* Responsive Adjustments */
        @media (max-width: 600px) {
            .mode-select {
                flex-direction: column;
                gap: 10px;
            }
            .size-3 { grid-template-columns: repeat(3, 70px); }
            .size-4 { grid-template-columns: repeat(4, 60px); }
            .size-5 { grid-template-columns: repeat(5, 50px); }
            .size-3 .tile { width: 70px; height: 70px; font-size: 24px; }
            .size-4 .tile { width: 60px; height: 60px; font-size: 18px; }
            .size-5 .tile { width: 50px; height: 50px; font-size: 16px; }
        }
    </style>
</head>
<body>
    <!-- Start Screen -->
    <div class="screen" id="start-screen">
        <h1 class="neon-text" style="font-size: 3rem;">Kannu's Puzzle Game</h1>
        <p style="font-size: 1.2rem; margin-bottom: 30px;">Select your game mode:</p>
        
        <div class="mode-select">
            <button class="mode-btn" data-size="3">1-8 (3×3)</button>
            <button class="mode-btn" data-size="4">1-15 (4×4)</button>
            <button class="mode-btn" data-size="5">1-24 (5×5)</button>
        </div>

        <div class="signature neon-text">Created by Kannu</div>
    </div>

    <!-- Game Screen -->
    <div class="screen hidden" id="game-screen">
        <div class="game-container">
            <h1 class="neon-text" id="game-title">Number Puzzle</h1>
            <div class="puzzle-board" id="board"></div>
            <div class="game-controls">
                <button class="control-btn" id="shuffle-btn">Shuffle</button>
                <button class="control-btn" id="menu-btn">Menu</button>
            </div>
            <p id="moves">Moves: <span id="move-count">0</span> <span class="move-limit" id="move-warning"></span></p>
        </div>
        <button class="share-btn" id="share-btn">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M4 12v8a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-8"></path>
                <polyline points="16 6 12 2 8 6"></polyline>
                <line x1="12" y1="2" x2="12" y2="15"></line>
            </svg>
            Share
        </button>
        <div class="signature neon-text">Created by Kannu</div>
    </div>

    <!-- Win Screen -->
    <div class="screen hidden" id="win-screen">
        <h1 class="neon-text" style="font-size: 3rem;">You Won! 🎉</h1>
        <p style="font-size: 1.5rem;" id="win-moves">Moves: 0</p>
        <button class="mode-btn" id="play-again-btn">Play Again</button>
        <button class="share-btn" style="position: relative; bottom: auto; left: auto; margin-top: 20px;" id="share-win-btn">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M4 12v8a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-8"></path>
                <polyline points="16 6 12 2 8 6"></polyline>
                <line x1="12" y1="2" x2="12" y2="15"></line>
            </svg>
            Share Victory
        </button>
        <div class="signature neon-text">Created by Kannu</div>
    </div>

    <!-- Lose Screen -->
    <div class="screen hidden" id="lose-screen">
        <h1 class="neon-text" style="font-size: 3rem;">Game Over! 😢</h1>
        <p style="font-size: 1.5rem;">Better luck next time!</p>
        <button class="mode-btn" id="try-again-btn">Try Again</button>
        <div class="signature neon-text">Created by Kannu</div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Elements
            const startScreen = document.getElementById('start-screen');
            const gameScreen = document.getElementById('game-screen');
            const winScreen = document.getElementById('win-screen');
            const loseScreen = document.getElementById('lose-screen');
            const board = document.getElementById('board');
            const shuffleBtn = document.getElementById('shuffle-btn');
            const menuBtn = document.getElementById('menu-btn');
            const moveCount = document.getElementById('move-count');
            const moveWarning = document.getElementById('move-warning');
            const winMoves = document.getElementById('win-moves');
            const playAgainBtn = document.getElementById('play-again-btn');
            const tryAgainBtn = document.getElementById('try-again-btn');
            const gameTitle = document.getElementById('game-title');
            const modeBtns = document.querySelectorAll('.mode-btn[data-size]');
            const shareBtn = document.getElementById('share-btn');
            const shareWinBtn = document.getElementById('share-win-btn');

            // Game Variables
            let moves = 0;
            let tiles = [];
            let emptyPos;
            let boardSize = 3;
            let moveLimit;
            let touchStartX, touchStartY;

            // Sound Effects
            const sounds = {
                move: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-arcade-game-jump-coin-216.mp3'),
                win: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-winning-chimes-2015.mp3'),
                lose: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-retro-arcade-lose-2027.mp3'),
                shuffle: new Audio('https://assets.mixkit.co/sfx/preview/mixkit-arcade-mechanical-bling-210.mp3')
            };

            // Preload sounds
            Object.values(sounds).forEach(sound => {
                sound.volume = 0.5;
                sound.load();
            });

            // Mode Selection
            modeBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    boardSize = parseInt(btn.dataset.size);
                    startGame();
                });
            });

            // Start Game
            function startGame() {
                startScreen.classList.add('hidden');
                gameScreen.classList.remove('hidden');
                
                // Set game parameters based on size
                if (boardSize === 3) {
                    moveLimit = 150;
                    gameTitle.textContent = "1-8 Puzzle";
                } else if (boardSize === 4) {
                    moveLimit = 250;
                    gameTitle.textContent = "1-15 Puzzle";
                } else {
                    moveLimit = 400;
                    gameTitle.textContent = "1-24 Puzzle";
                }
                
                initBoard();
                shuffleBoard();
            }

            // Initialize Board
            function initBoard() {
                board.innerHTML = '';
                board.className = `puzzle-board size-${boardSize}`;
                tiles = [];
                moves = 0;
                moveCount.textContent = moves;
                moveWarning.textContent = '';
                emptyPos = (boardSize * boardSize) - 1; // Last tile is empty
                
                const totalTiles = boardSize * boardSize;
                
                for (let i = 0; i < totalTiles; i++) {
                    const tile = document.createElement('div');
                    tile.className = i === emptyPos ? 'tile empty' : `tile tile-${i + 1}`;
                    tile.textContent = i !== emptyPos ? i + 1 : '';
                    tile.addEventListener('click', () => moveTile(i));
                    // Swipe Events
                    tile.addEventListener('touchstart', handleTouchStart);
                    tile.addEventListener('touchend', handleTouchEnd);
                    board.appendChild(tile);
                    tiles.push(tile);
                }
            }

            // Touch Handling for Swipe
            function handleTouchStart(e) {
                touchStartX = e.touches[0].clientX;
                touchStartY = e.touches[0].clientY;
            }

            function handleTouchEnd(e) {
                if (!touchStartX || !touchStartY) return;
                const touchEndX = e.changedTouches[0].clientX;
                const touchEndY = e.changedTouches[0].clientY;
                const diffX = touchStartX - touchEndX;
                const diffY = touchStartY - touchEndY;

                // Determine swipe direction
                if (Math.abs(diffX) > Math.abs(diffY)) {
                    if (diffX > 0) tryMove('left');
                    else tryMove('right');
                } else {
                    if (diffY > 0) tryMove('up');
                    else tryMove('down');
                }
            }

            // Try moving based on swipe direction
            function tryMove(direction) {
                const row = Math.floor(emptyPos / boardSize);
                const col = emptyPos % boardSize;
                let targetIndex = -1;

                switch (direction) {
                    case 'up': if (row < boardSize-1) targetIndex = emptyPos + boardSize; break;
                    case 'down': if (row > 0) targetIndex = emptyPos - boardSize; break;
                    case 'left': if (col < boardSize-1) targetIndex = emptyPos + 1; break;
                    case 'right': if (col > 0) targetIndex = emptyPos - 1; break;
                }

                if (targetIndex !== -1) moveTile(targetIndex);
            }

            // Move Tile Logic
            function moveTile(index) {
                const row = Math.floor(index / boardSize);
                const col = index % boardSize;
                const emptyRow = Math.floor(emptyPos / boardSize);
                const emptyCol = emptyPos % boardSize;

                if (
                    (Math.abs(row - emptyRow) === 1 && col === emptyCol) ||
                    (Math.abs(col - emptyCol) === 1 && row === emptyRow)
                ) {
                    sounds.move.currentTime = 0;
                    sounds.move.play();

                    // Swap tile with empty
                    tiles[emptyPos].textContent = tiles[index].textContent;
                    tiles[emptyPos].className = `tile tile-${tiles[index].textContent}`;
                    tiles[index].textContent = '';
                    tiles[index].className = 'tile empty';
                    emptyPos = index;
                    moves++;
                    moveCount.textContent = moves;

                    checkWin();
                    checkMoveLimit();
                }
            }

            // Shuffle Board
            function shuffleBoard() {
                sounds.shuffle.play();
                moves = 0;
                moveCount.textContent = moves;
                moveWarning.textContent = '';
                
                // Random moves to shuffle
                for (let i = 0; i < 500; i++) {
                    const possibleMoves = [];
                    const row = Math.floor(emptyPos / boardSize);
                    const col = emptyPos % boardSize;

                    // Check possible moves
                    if (row > 0) possibleMoves.push(emptyPos - boardSize); // Up
                    if (row < boardSize-1) possibleMoves.push(emptyPos + boardSize); // Down
                    if (col > 0) possibleMoves.push(emptyPos - 1); // Left
                    if (col < boardSize-1) possibleMoves.push(emptyPos + 1); // Right

                    const randomMove = possibleMoves[Math.floor(Math.random() * possibleMoves.length)];
                    // Simulate move without counting
                    tiles[emptyPos].textContent = tiles[randomMove].textContent;
                    tiles[emptyPos].className = `tile tile-${tiles[randomMove].textContent}`;
                    tiles[randomMove].textContent = '';
                    tiles[randomMove].className = 'tile empty';
                    emptyPos = randomMove;
                }
            }

            // Check Win
            function checkWin() {
                const totalTiles = boardSize * boardSize - 1;
                for (let i = 0; i < totalTiles; i++) {
                    if (tiles[i].textContent !== (i + 1).toString()) return;
                }
                sounds.win.play();
                winMoves.textContent = `Moves: ${moves}`;
                gameScreen.classList.add('hidden');
                winScreen.classList.remove('hidden');
            }

            // Check Move Limit
            function checkMoveLimit() {
                if (moves >= moveLimit) {
                    sounds.lose.play();
                    moveWarning.textContent = "Move limit reached!";
                    setTimeout(() => {
                        gameScreen.classList.add('hidden');
                        loseScreen.classList.remove('hidden');
                    }, 500);
                }
            }

            // Share Functionality
            function shareGame(isWin = false) {
                const gameUrl = window.location.href.split('?')[0];
                const shareText = isWin 
                    ? `I solved Kannu's ${boardSize}x${boardSize} puzzle in ${moves} moves! Can you beat me?` 
                    : `Try Kannu's awesome puzzle game! ${boardSize}x${boardSize} challenge awaits!`;
                
                if (navigator.share) {
                    navigator.share({
                        title: "Kannu's Puzzle Game",
                        text: shareText,
                        url: gameUrl
                    }).catch(err => {
                        copyToClipboard(`${shareText}\n\nPlay here: ${gameUrl}`);
                    });
                } else {
                    copyToClipboard(`${shareText}\n\nPlay here: ${gameUrl}`);
                }
            }

            function copyToClipboard(text) {
                const textarea = document.createElement('textarea');
                textarea.value = text;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                alert("Link copied to clipboard! Share it with your friends.");
            }

            // Button Events
            shuffleBtn.addEventListener('click', shuffleBoard);
            menuBtn.addEventListener('click', () => {
                gameScreen.classList.add('hidden');
                startScreen.classList.remove('hidden');
            });
            playAgainBtn.addEventListener('click', () => {
                winScreen.classList.add('hidden');
                startGame();
            });
            tryAgainBtn.addEventListener('click', () => {
                loseScreen.classList.add('hidden');
                startGame();
            });
            shareBtn.addEventListener('click', () => shareGame(false));
            shareWinBtn.addEventListener('click', () => shareGame(true));
        });
    </script>
</body>
</html>
