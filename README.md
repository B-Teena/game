# game
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chess Game</title>
    <style>
        .chessboard {
            display: grid;
            grid-template-columns: repeat(8, 50px);
            grid-template-rows: repeat(8, 50px);
        }

        .chessboard div {
            width: 50px;
            height: 50px;
            text-align: center;
            vertical-align: middle;
            font-size: 24px;
            line-height: 50px;
        }

        .white {
            background-color: #f0d9b5;
        }

        .black {
            background-color: #b58863;
        }
    </style>
</head>
<body>
    <div class="chessboard" id="board"></div>

    <script>
        const board = document.getElementById('board');
        let isWhiteTurn = true;

        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                const cell = document.createElement('div');
                cell.dataset.row = row;
                cell.dataset.col = col;
                cell.classList.add((row + col) % 2 === 0 ? 'white' : 'black');
                cell.addEventListener('click', handleCellClick);
                board.appendChild(cell);
            }
        }

        function handleCellClick(event) {
            const cell = event.target;
            const row = cell.dataset.row;
            const col = cell.dataset.col;

            if (cell.classList.contains('selected')) {
                // If already selected, deselect it
                cell.classList.remove('selected');
            } else if (cell.textContent) {
                // If the cell has a piece, select it
                clearSelection();
                cell.classList.add('selected');
            } else if (cell.classList.contains('move')) {
                // If the cell is a valid move, make the move
                const selectedCell = document.querySelector('.selected');
                selectedCell.textContent = '';
                cell.textContent = selectedCell.textContent;
                selectedCell.textContent = '';
                cell.classList.remove('move');
                selectedCell.classList.remove('selected');
                isWhiteTurn = !isWhiteTurn;
            }
        }

        function clearSelection() {
            const selectedCell = document.querySelector('.selected');
            if (selectedCell) {
                selectedCell.classList.remove('selected');
                clearValidMoves();
            }
        }

        function clearValidMoves() {
            const validMoves = document.querySelectorAll('.move');
            validMoves.forEach(move => move.classList.remove('move'));
        }

        // You'll need to implement the chess piece movement logic here.

    </script>
</body>
</html>
