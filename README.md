# Tic-tac-toe-web-application
To build a tic-tac-toe web application
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="board">
        <div class="cell" id="cell-0"></div>
        <div class="cell" id="cell-1"></div>
        <div class="cell" id="cell-2"></div>
        <div class="cell" id="cell-3"></div>
        <div class="cell" id="cell-4"></div>
        <div class="cell" id="cell-5"></div>
        <div class="cell" id="cell-6"></div>
        <div class="cell" id="cell-7"></div>
        <div class="cell" id="cell-8"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

#board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-gap: 5px;
    background-color: #333;
    padding: 5px;
}

.cell {
    width: 100px;
    height: 100px;
    background-color: #ddd;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 3em;
    cursor: pointer;
}

.cell:hover {
    background-color: #ccc;
}

document.addEventListener('DOMContentLoaded', () => {
    const cells = document.querySelectorAll('.cell');
    let currentPlayer = 'X';
    let gameState = ['', '', '', '', '', '', '', '', ''];
    let gameActive = true;

    const winningConditions = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
    ];

    const handleCellClick = (clickedCellEvent) => {
        const clickedCell = clickedCellEvent.target;
        const clickedCellIndex = parseInt(clickedCell.getAttribute('id').substring(5));

        if (gameState[clickedCellIndex] !== '' || !gameActive) {
            return;
        }

        gameState[clickedCellIndex] = currentPlayer;
        clickedCell.textContent = currentPlayer;
        clickedCell.style.color = currentPlayer === 'X' ? 'blue' : 'red';

        if (checkWin()) {
            announceResult(`${currentPlayer} wins!`);
            gameActive = false;
            return;
        }

        if (checkDraw()) {
            announceResult(`It's a draw!`);
            gameActive = false;
            return;
        }

        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    };

    const checkWin = () => {
        for (let condition of winningConditions) {
            const [a, b, c] = condition;
            if (gameState[a] !== '' && gameState[a] === gameState[b] && gameState[a] === gameState[c]) {
                return true;
            }
        }
        return false;
    };

    const checkDraw = () => {
        return gameState.every(cell => cell !== '');
    };

    const announceResult = (message) => {
        alert(message);
    };

    cells.forEach(cell => cell.addEventListener('click', handleCellClick));
});
