# TIC_TAC_TOE_GAME
TIC TAC TOE is a game in which two players take turns in drawing either an 'O' or an 'X' in one square of a grid consisting of nine squares.

//html code
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Tic Tac Toe</title>
    <link rel="stylesheet" href="style.css">
</head>
<body >
    <section>
        <h1 class="game--title">Tic Tac Toe</h1>
        <div class="game--container">
            <div data-cell-index="0" class="cell" id="a"></div>
            <div data-cell-index="1" class="cell" id="b"></div>
            <div data-cell-index="2" class="cell" id="c"></div>
            <div data-cell-index="3" class="cell" id="d"></div>
            <div data-cell-index="4" class="cell" id="e"></div>
            <div data-cell-index="5" class="cell" id="f"></div>
            <div data-cell-index="6" class="cell" id="g"></div>
            <div data-cell-index="7" class="cell" id="h"></div>
            <div data-cell-index="8" class="cell" id="i"></div>
        </div>
        <h2 class="game--status"></h2>
        <button class="game--restart">Restart Game</button>
    </section>

    <script src="script.js"></script>
</body>
</html>


//CSS CODE

body {
    font-family: "Arial", sans-serif;
    background-image: url("https://cdn.borntoengineer.com/2017/10/video-games.jpeg");
    background-size: cover;
  } 
  
  section {
    text-align:center;
  }
  
  .game--title {
    font-size: 90px;
    color: black;
    margin: 10px auto;
  }
  .game--title{
    --h: 1.2em;   
    linea-height: var(--h);
    color: #0000;
    overflow: hidden;
    text-shadow: 
      0 var(--_t,var(--h)) #fff,
      0 0 var(--_c,#000);
    background: 
      linear-gradient(#1095c1 0 0) 
      bottom/100% var(--_d, 0) no-repeat;
    transition: 0.3s;
  }
  .game--title:hover {
    --_d: 100%;
    --_t: 0;
    --_c: #0000;
  }
  
  
  .game--container {
    display: grid;
    grid-template-columns: repeat(3, auto);
    width: 306px;
    margin: 10px auto;
    background-color: #11213a;
    color: black;
  }
  
  .cell {
    font-family: "Permanent Marker", cursive;
    width: 100px;
    height: 100px;
    box-shadow: 2px 2px 2px 2px #ecd7ba;
    border: 2px solid #ecd7ba;
    cursor: pointer;
    line-height: 100px;
    font-size: 60px;
  }
  
  .game--status {
    font-size: 50px;
    color: red;
    margin: 20px auto;
  }
  
  .game--restart {
    background-color: green;
    width: 200px;
    height: 50px;
    font-size: 25px;
    color: black;
    border-radius: 20%;
  }
  
  #a{
    background-image: url("https://wallpapercave.com/wp/wp7299410.jpg");
    background-size: cover;
    
  }
  #b{
    background-image: url("https://tse1.mm.bing.net/th?id=OIP.kI0VhFaMsf4wqrEc8bxVkgHaEo&pid=Api&P=0&h=180");
    background-size: cover;
  }
  #c{
    background-image: url("http://wallpapercave.com/wp/wc1730209.jpg");
    background-size:cover;
  }
  #d{
    background-image: url("https://tse1.mm.bing.net/th?id=OIP.J7TVYJcCGjh_MOsJLDXttwHaGl&pid=Api&P=0&h=180");
    background-size: cover;
  }
  #e{
    background-image: url("https://tse1.mm.bing.net/th?id=OIP.pIWBHiuBZAYZYCrzjWk2-AHaF7&pid=Api&P=0&h=180");
    background-size: cover;
  }
  #f{
    background-image: url("https://tse3.mm.bing.net/th?id=OIP.WdJ8NpGUBAm0_fUZ3BbMGQHaEo&pid=Api&P=0&h=180");
    background-size: cover;
  }
  #g{
    background-image: url("https://vignette.wikia.nocookie.net/p__/images/3/38/Mantis_(Avengers_Infinity_War_Textless).png/revision/latest/scale-to-width-down/201?cb=20180402090641&path-prefix=protagonist");
    background-size: cover;
  }
  #h{
    background-image: url("https://tse2.mm.bing.net/th?id=OIP.zClzY-B13HIb-WdI-q2FXgHaEK&pid=Api&P=0&h=180");
    background-size: cover;
  }
  #i{
    background-image: url("https://tse4.mm.bing.net/th?id=OIP.nsQhj3LFD-wwIYnexcJPkQHaEK&pid=Api&P=0&h=180");
    background-size: cover;
  }

  //javascript code

  const statusDisplay = document.querySelector('.game--status');

let gameActive = true;
let currentPlayer = "X";
let gameState = ["", "", "", "", "", "", "", "", ""];

const winningMessage = () => `Player ${currentPlayer} has won!`;
const drawMessage = () => `Game ended in a draw!`;
const currentPlayerTurn = () => `It's ${currentPlayer}'s turn`;

statusDisplay.innerHTML = currentPlayerTurn();

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

function handleCellPlayed(clickedCell, clickedCellIndex) {
    gameState[clickedCellIndex] = currentPlayer;
    clickedCell.innerHTML = currentPlayer;
}

function handlePlayerChange() {
    currentPlayer = currentPlayer === "X" ? "O" : "X";
    statusDisplay.innerHTML = currentPlayerTurn();
}

function handleResultValidation() {
    let roundWon = false;
    for (let i = 0; i <= 7; i++) {
        const winCondition = winningConditions[i];
        let a = gameState[winCondition[0]];
        let b = gameState[winCondition[1]];
        let c = gameState[winCondition[2]];
        if (a === '' || b === '' || c === '') {
            continue;
        }
        if (a === b && b === c) {
            roundWon = true;
            break
        }
    }

    if (roundWon) {
        statusDisplay.innerHTML = winningMessage();
        gameActive = false;
        return;
    }

    let roundDraw = !gameState.includes("");
    if (roundDraw) {
        statusDisplay.innerHTML = drawMessage();
        gameActive = false;
        return;
    }

    handlePlayerChange();
}

function handleCellClick(clickedCellEvent) {
    const clickedCell = clickedCellEvent.target;
    const clickedCellIndex = parseInt(clickedCell.getAttribute('data-cell-index'));

    if (gameState[clickedCellIndex] !== "" || !gameActive) {
        return;
    }

    handleCellPlayed(clickedCell, clickedCellIndex);
    handleResultValidation();
}

function handleRestartGame() {
    gameActive = true;
    currentPlayer = "X";
    gameState = ["", "", "", "", "", "", "", "", ""];
    statusDisplay.innerHTML = currentPlayerTurn();
    document.querySelectorAll('.cell').forEach(cell => cell.innerHTML = "");
}


document.querySelectorAll('.cell').forEach(cell => cell.addEventListener('click', handleCellClick));
document.querySelector('.game--restart').addEventListener('click', handleRestartGame);
