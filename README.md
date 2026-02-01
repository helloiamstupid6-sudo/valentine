# valentine
A tiny Valentine surprise 💕
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>For You 💗</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Name Access -->
  <div class="card" id="nameCard">
    <h1>Enter your name 💕</h1>
    <input type="text" id="nameInput" placeholder="Type your name">
    <button onclick="checkName()">Enter</button>
    <p id="error"></p>
  </div>

  <!-- Valentine Question -->
  <div class="card hidden" id="valentineCard">
    <h1>Will you be my Valentine? 💘</h1>
    <div class="buttons">
      <button id="yesBtn">YES 💖</button>
      <button id="noBtn">No 🙃</button>
    </div>
    <p id="message"></p>
  </div>

  <canvas id="confetti"></canvas>

  <script src="script.js"></script>
</body>
</html>
body {
  margin: 0;
  height: 100vh;
  background: pink;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
}

.card {
  background: white;
  padding: 40px;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 10px 25px rgba(0,0,0,0.2);
}

.hidden {
  display: none;
}

input {
  padding: 10px;
  width: 200px;
  margin-top: 10px;
  border-radius: 10px;
  border: 1px solid #ccc;
}

button {
  padding: 12px 25px;
  margin: 10px;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  font-size: 16px;
}

#yesBtn {
  background: #ff4d6d;
  color: white;
}

#noBtn {
  background: #ddd;
}

#message {
  font-size: 22px;
  color: #ff4d6d;
  margin-top: 20px;
}

canvas {
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
}
const nameCard = document.getElementById("nameCard");
const valentineCard = document.getElementById("valentineCard");
const nameInput = document.getElementById("nameInput");
const error = document.getElementById("error");

const yesBtn = document.getElementById("yesBtn");
const noBtn = document.getElementById("noBtn");
const message = document.getElementById("message");

let yesSize = 16;

// Name check
function checkName() {
  if (nameInput.value.toLowerCase() === "ahamed") {
    nameCard.classList.add("hidden");
    valentineCard.classList.remove("hidden");
  } else {
    error.textContent = "Access denied 🙃";
    error.style.color = "red";
  }
}

// YES click
yesBtn.addEventListener("click", () => {
  message.textContent = "YAYYYY 💕🎉";
  startConfetti();
});

// NO click → YES grows
noBtn.addEventListener("click", () => {
  yesSize += 10;
  yesBtn.style.fontSize = yesSize + "px";
});

/* Confetti */
const canvas = document.getElementById("confetti");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

function startConfetti() {
  const pieces = [];
  for (let i = 0; i < 200; i++) {
    pieces.push({
      x: canvas.width / 2,
      y: canvas.height / 2,
      size: Math.random() * 8 + 4,
      speedX: (Math.random() - 0.5) * 12,
      speedY: (Math.random() - 0.5) * 12,
      color: `hsl(${Math.random() * 360}, 100%, 60%)`
    });
  }

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    pieces.forEach(p => {
      ctx.fillStyle = p.color;
      ctx.fillRect(p.x, p.y, p.size, p.size);
      p.x += p.speedX;
      p.y += p.speedY;
      p.speedY += 0.3;
    });
    requestAnimationFrame(animate);
  }

  animate();
}
