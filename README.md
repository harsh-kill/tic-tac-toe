<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #667eea, #764ba2);
        }

        .game {
            background: white;
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
        }

        h1 {
            margin-bottom: 10px;
            color: #333;
        }

        #status {
            margin-bottom: 20px;
            font-size: 20px;
            font-weight: bold;
            color: #555;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 8px;
            margin-bottom: 20px;
        }

        .cell {
            border: none;
            border-radius: 10px;
            background: #f0f0f0;
            font-size: 40px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }

        .cell:hover {
            background: #ddd;
        }

        .cell.x {
            color: #e74c3c;
        }

        .cell.o {
            color: #3498db;
        }

        #reset {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            background: #667eea;
            color: white;
            font-size: 16px;
            cursor: pointer;
        }

        #reset:hover {
            background: #5367d8;
        }

        @media (max-width: 400px) {
            .board {
                grid-template-columns: repeat(3, 80px);
                grid-template-rows: repeat(3, 80px);
            }

            .cell {
                font-size: 30px;
            }
        }
    </style>
</head>

<body>

    <div class="game">

        <h1>Tic Tac Toe</h1>

        <p id="status">Player X's Turn</p>

        <div class="board">
            <button class="cell"></button>
            <button class="cell"></button>
            <button class="cell"></button>

            <button class="cell"></button>
            <button class="cell"></button>
            <button class="cell"></button>

            <button class="cell"></button>
            <button class="cell"></button>
            <button class="cell"></button>
        </div>

        <button id="reset">Restart Game</button>

    </div>


    <script>

        const cells = document.querySelectorAll(".cell");
        const statusText = document.getElementById("status");
        const resetButton = document.getElementById("reset");

        let currentPlayer = "X";
        let gameActive = true;

        let board = ["", "", "", "", "", "", "", ""];

        const winningPatterns = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],

            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],

            [0, 4, 8],
            [2, 4, 6]
        ];


        cells.forEach((cell, index) => {

            cell.addEventListener("click", () => {

                if (board[index] !== "" || !gameActive) {
                    return;
                }

                board[index] = currentPlayer;
                cell.textContent = currentPlayer;

                cell.classList.add(currentPlayer.toLowerCase());

                checkWinner();

            });

        });


        function checkWinner() {

            let winner = null;

            for (let pattern of winningPatterns) {

                const a = board[pattern[0]];
                const b = board[pattern[1]];
                const c = board[pattern[2]];

                if (a !== "" && a === b && b === c) {
                    winner = a;
                    break;
                }
            }

            if (winner) {

                statusText.textContent = `🎉 Player ${winner} Wins!`;
                gameActive = false;
                return;

            }

            if (!board.includes("")) {

                statusText.textContent = "🤝 Game Draw!";
                gameActive = false;
                return;

            }

            currentPlayer = currentPlayer === "X" ? "O" : "X";

            statusText.textContent = `Player ${currentPlayer}'s Turn`;

        }


        resetButton.addEventListener("click", resetGame);


        function resetGame() {

            board = ["", "", "", "", "", "", "", ""];

            currentPlayer = "X";
            gameActive = true;

            statusText.textContent = "Player X's Turn";

            cells.forEach(cell => {

                cell.textContent = "";

                cell.classList.remove("x");
                cell.classList.remove("o");

            });

        }

    </script>

</body>
</html>

