‏<!DOCTYPE html>
‏<html lang="ar">
‏<head>
‏<meta charset="UTF-8">
‏<title>XO AI - 3 مستويات</title>
‏<style>
‏  body{background:#0f0f1a;color:white;font-family:'Cairo',sans-serif;display:flex;flex-direction:column;align-items:center;justify-content:center;height:100vh;margin:0}
‏  h1{color:#00f5d4}
‏.score{font-size:20px;margin:10px;color:#ff2e63}
‏.board{display:grid;grid-template-columns:repeat(3,100px);gap:8px}
‏.box{width:100px;height:100px;background:#1e1e2f;display:flex;align-items:center;justify-content:center;font-size:40px;font-weight:bold;cursor:pointer;border-radius:12px;transition:0.2s}
‏.box:hover{background:#2a2a40;transform:scale(1.05)}
‏  button,select{margin:5px;padding:10px 20px;border:none;border-radius:8px;background:#00f5d4;color:#000;font-weight:bold;cursor:pointer}
‏</style>
‏</head>
‏<body>

‏<h1>لعبة XO 🤖</h1>
‏<select id="level" onchange="changeLevel()">
‏  <option value="easy">سهل 😊</option>
‏  <option value="medium">متوسط 🤔</option>
‏  <option value="hard">مستحيل 😈</option>
‏</select>

‏<div class="score">X: <span id="scoreX">0</span> | O: <span id="scoreO">0</span> | تعادل: <span id="scoreDraw">0</span></div>
‏<div class="board" id="board"></div>
‏<button onclick="resetGame()">لعبة جديدة</button>

‏<script>
‏let turn = "X"
‏let gameOver = false
‏let vsBot = true
‏let level = "easy" // المستوى الحالي
‏let score = {X:0, O:0, draw:0}
‏let board = ["","","","","","","","",""]
‏let wins = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]]

// نرسم البورد
‏for(let i=0; i<9; i++){
‏  let div = document.createElement("div")
‏  div.className = "box"
‏  div.id = i
‏  div.onclick = ()=>play(i)
‏  document.getElementById("board").appendChild(div)
}

‏function changeLevel(){
‏  level = document.getElementById("level").value
‏  resetGame()
}

‏function play(i){
‏  let box = document.getElementById(i)
‏  if(box.innerHTML == "" &&!gameOver){
‏    box.innerHTML = turn
‏    board[i] = turn
‏    box.style.color = turn == "X"? "#00f5d4" : "#ff2e63"

‏    if(checkWinner()){
‏      alert(turn + " كسب! 🎉")
‏      score++
‏      updateScore()
‏      gameOver = true
‏    } else if(isDraw()){
‏      alert("تعادل! 🤝")
‏      score.draw++
‏      updateScore()
‏      gameOver = true
‏    } else {
‏      turn = (turn == "X")? "O" : "X"
‏      if(vsBot && turn == "O" &&!gameOver) setTimeout(botMove, 400)
    }
  }
}

‏function checkWinner(){
‏  for(let combo of wins){
‏    if(board[combo[0]] == board[combo[1]] && board[combo[1]] == board[combo[2]] && board[combo[0]]!= "") return true
  }
‏  return false
}

‏function isDraw(){ return board.every(cell => cell!= "") }

‏function updateScore(){
‏  document.getElementById("scoreX").innerText = score.X
‏  document.getElementById("scoreO").innerText = score.O
‏  document.getElementById("scoreDraw").innerText = score.draw
}

‏function resetGame(){
‏  board = ["","","","","","","","",""]
‏  gameOver = false
‏  turn = "X"
‏  for(let i=0; i<9; i++) document.getElementById(i).innerHTML = ""
}

// ========== البوت ب 3 مستويات ==========
‏function botMove(){
‏  let move
‏  if(level == "easy") move = randomMove() // عشوائي
‏  if(level == "medium") move = Math.random() > 0.5? bestMove() : randomMove() // نص نص
‏  if(level == "hard") move = bestMove() // Minimax

‏  play(move)
}

‏function randomMove(){
‏  let empty = []
‏  for(let i=0; i<9; i++) if(board[i] == "") empty.push(i)
‏  return empty[Math.floor(Math.random()*empty.length)]
}

‏function bestMove(){ // ده الـ Minimax بتاع المستحيل
‏  let bestScore = -Infinity
‏  let move
‏  for(let i=0; i<9; i++){
‏    if(board[i] == ""){
‏      board[i] = "O"
‏      let scoreVal = minimax(board, 0, false)
‏      board[i] = ""
‏      if(scoreVal > bestScore){
‏        bestScore = scoreVal
‏        move = i
      }
    }
  }
‏  return move
}

‏function minimax(b, depth, isMaximizing){
‏  let result = checkWinnerMinimax(b)
‏  if(result!== null){
‏    if(result == "O") return 10 - depth
‏    if(result == "X") return depth - 10
‏    if(result == "draw") return 0
  }
‏  if(isMaximizing){
‏    let bestScore = -Infinity
‏    for(let i=0; i<9; i++){
‏      if(b[i] == ""){ b[i] = "O"; let s = minimax(b, depth+1, false); b[i] = ""; bestScore = Math.max(s, bestScore) }
    }
‏    return bestScore
‏  } else {
‏    let bestScore = Infinity
‏    for(let i=0; i<9; i++){
‏      if(b[i] == ""){ b[i] = "X"; let s = minimax(b, depth+1, true); b[i] = ""; bestScore = Math.min(s, bestScore) }
    }
‏    return bestScore
  }
}

‏function checkWinnerMinimax(b){
‏  for(let combo of wins){
‏    if(b[combo[0]] == b[combo[1]] && b[combo[1]] == b[combo[2]] && b[combo[0]]!= "") return b[combo[0]]
  }
‏  if(b.every(cell => cell!= "")) return "draw"
‏  return null
}
‏</script>
‏</body>
‏</html>
- [ ] 
