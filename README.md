# PRODIGY_WD_03
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <link rel="stylesheet" href="styles.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #282c34;
            color: #ffffff;
        }
        h1 {
            margin: 20px 0;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
            justify-content: center;
            align-items: center;
        }
        .cell {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100px;
            height: 100px;
            background-color: #61dafb;
            border: 2px solid #000;
            font-size: 2em;
            cursor: pointer;
        }
        .cell.taken {
            pointer-events: none;
        }
        #restart {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 1em;
            background-color: #61dafb;
            border: none;
            cursor: pointer;
        }
        #restart:hover {
            background-color: #21a1f1;
        }
    </style>
</head>
<body>
    <h1>Tic-Tac-Toe</h1>
    <div class="board" id="board">
        <div class="cell" data-index="0"></div>
        <div class="cell" data-index="1"></div>
        <div class="cell" data-index="2"></div>
        <div class="cell" data-index="3"></div>
        <div class="cell" data-index="4"></div>
        <div class="cell" data-index="5"></div>
        <div class="cell" data-index="6"></div>
        <div class="cell" data-index="7"></div>
        <div class="cell" data-index="8"></div>
    </div>
    <h2 id="status"></h2>
    <button id="restart">Restart Game</button>

    <script>
        const cells = document.querySelectorAll('.cell');
        const statusText = document.getElementById('status');
        const restartBtn = document.getElementById('restart');
        let currentPlayer = 'X';
        let board = Array(9).fill(null);
        
        const winPatterns = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],
            [0, 3, 6], [1, 4, 7], [2, 5, 8],
            [0, 4, 8], [2, 4, 6]
        ];
        
        function checkWinner() {
            for (const pattern of winPatterns) {
                const [a, b, c] = pattern;
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    statusText.innerText = `${board[a]} wins!`;
                    cells.forEach(cell => cell.classList.add('taken'));
                    return true;
                }
            }
            if (!board.includes(null)) {
                statusText.innerText = "It's a draw!";
                return true;
            }
            return false;
        }
        
        function handleClick(e) {
            const index = e.target.dataset.index;
            if (!board[index]) {
                board[index] = currentPlayer;
                e.target.innerText = currentPlayer;
                e.target.classList.add('taken');
                if (checkWinner()) return;
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                statusText.innerText = `Player ${currentPlayer}'s turn`;
            }
        }
        
        function restartGame() {
            board.fill(null);
            cells.forEach(cell => {
                cell.innerText = '';
                cell.classList.remove('taken');
            });
            currentPlayer = 'X';
            statusText.innerText = "Player X's turn";
        }
        
        cells.forEach(cell => cell.addEventListener('click', handleClick));
        restartBtn.addEventListener('click', restartGame);
        restartGame();
    </script>
</body>
</html>
