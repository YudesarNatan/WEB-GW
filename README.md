<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Game Tangkap Kotak</title>
  <style>
    body {
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      height: 100vh;
      background-color: #f0f0f0;
      font-family: Arial, sans-serif;
    }
    #gameArea {
      width: 400px;
      height: 400px;
      border: 2px solid #333;
      position: relative;
      background-color: white;
    }
    #player {
      width: 50px;
      height: 50px;
      background-color: #4CAF50;
      position: absolute;
      bottom: 10px;
      left: 175px;
    }
    #box {
      width: 30px;
      height: 30px;
      background-color: #f44336;
      position: absolute;
      top: 0;
      left: 50%;
    }
    #score {
      margin-top: 20px;
      font-size: 1.2rem;
    }
  </style>
</head>
<body>
  <h2>Game Tangkap Kotak 🎮</h2>
  <div id="gameArea">
    <div id="player"></div>
    <div id="box"></div>
  </div>
  <div id="score">Skor: 0</div>

  <script>
    const player = document.getElementById('player');
    const box = document.getElementById('box');
    const scoreDisplay = document.getElementById('score');
    const gameArea = document.getElementById('gameArea');

    let playerX = 175;
    let boxX = Math.random() * 370;
    let boxY = 0;
    let score = 0;

    // Gerakan pemain
    document.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowLeft' && playerX > 0) {
        playerX -= 15;
      } else if (e.key === 'ArrowRight' && playerX < 350) {
        playerX += 15;
      }
      player.style.left = playerX + 'px';
    });

    // Gerakan kotak jatuh
    function dropBox() {
      boxY += 5;
      box.style.top = boxY + 'px';
      box.style.left = boxX + 'px';

      // Jika kotak mencapai bawah
      if (boxY > 350) {
        // Cek tabrakan
        if (boxX > playerX && boxX < playerX + 50) {
          score++;
          scoreDisplay.textContent = 'Skor: ' + score;
        }
        resetBox();
      }

      requestAnimationFrame(dropBox);
    }

    // Reset posisi kotak
    function resetBox() {
      boxY = 0;
      boxX = Math.random() * 370;
    }

    dropBox();
  </script>
</body>
</html>
