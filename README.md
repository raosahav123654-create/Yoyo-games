# Yoyo-games
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Anime Ludo - Battle of Legends</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #100d20;
  color: white;
  font-family: Arial, sans-serif;
  text-align: center;
}

h1 {
  color: #ffcc33;
  text-shadow: 0 0 15px #ff6600;
}

.board {
  width: 90vw;
  max-width: 390px;
  aspect-ratio: 1;
  margin: 20px auto;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: repeat(5, 1fr);
  gap: 4px;
  background: #29213e;
  padding: 6px;
  border: 3px solid #a855f7;
  border-radius: 15px;
}

.cell {
  background: #45365f;
  border-radius: 8px;
  display: grid;
  place-items: center;
  font-size: 24px;
}

.red { background: #d83b58; }
.blue { background: #287bd5; }
.green { background: #249c72; }
.yellow { background: #c99a23; }

.player {
  font-size: 26px;
  cursor: pointer;
  filter: drop-shadow(0 0 7px white);
}

button {
  padding: 13px 25px;
  background: linear-gradient(45deg,#a855f7,#ec4899);
  border: none;
  border-radius: 12px;
  color: white;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
}

#result {
  color: #ffcc33;
  font-size: 18px;
  margin: 15px;
}
</style>
</head>

<body>

<h1>⚔ ANIME LUDO ⚔</h1>
<p>Battle of Legends</p>

<div class="board" id="board"></div>

<h2>🎲 Dice: <span id="dice">1</span></h2>
<button onclick="rollDice()">ROLL DICE</button>

<p id="result">Red Ninja's Turn</p>

<script>
const board = document.getElementById("board");

const icons = ["🥷","⚡","🔥","🐉"];
const colors = ["red","blue","green","yellow"];

let positions = [0,0,0,0];
let currentPlayer = 0;
let dice = 1;

const paths = [
  [0,1,2,3,4,9,14,19,24,23,22,21,20,15,10,5],
  [4,3,2,1,0,5,10,15,20,21,22,23,24,19,14,9],
  [20,15,10,5,0,1,2,3,4,9,14,19,24,23,22,21],
  [24,19,14,9,4,3,2,1,0,5,10,15,20,21,22,23]
];

function drawBoard() {
  board.innerHTML = "";

  for (let i=0; i<25; i++) {
    const cell = document.createElement("div");
    cell.className = "cell";

    colors.forEach((color,p) => {
      if (paths[p][positions[p] % paths[p].length] === i) {
        const token = document.createElement("span");
        token.className = "player";
        token.textContent = icons[p];
        token.style.color = color;
        token.onclick = () => movePlayer(p);
        cell.appendChild(token);
      }
    });

    board.appendChild(cell);
  }
}

function rollDice() {
  dice = Math.floor(Math.random()*6)+1;
  document.getElementById("dice").textContent = dice;

  document.getElementById("result").textContent =
    colors[currentPlayer].toUpperCase() +
    " Ninja rolled " + dice + "!";
}

function movePlayer(p) {
  if (p !== currentPlayer) return;

  positions[p] += dice;

  if (positions[p] >= 16) {
    positions[p] = 0;
  }

  drawBoard();

  currentPlayer = (currentPlayer+1)%4;

  document.getElementById("result").textContent =
    colors[currentPlayer].toUpperCase() + " Ninja's Turn";
}

drawBoard();
</script>

</body>
</html>
