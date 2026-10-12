<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Anime Energy Animation</title>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  overflow: hidden;
  background: radial-gradient(circle, #240617, #03030c 70%);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
  color: white;
}

.scene {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.title {
  position: absolute;
  top: 10%;
  font-size: 24px;
  letter-spacing: 3px;
  color: #ff416d;
  text-shadow: 0 0 15px #ff174f;
  animation: pulse 2s infinite alternate;
}

.ring {
  width: 250px;
  height: 250px;
  position: relative;
  border: 5px solid #ff174f;
  border-radius: 50%;
  box-shadow:
    0 0 15px #ff174f,
    0 0 40px #ff174f,
    inset 0 0 25px #ff174f;
  animation: rotate 5s linear infinite,
             breathe 2s ease-in-out infinite alternate;
}

.ring::before,
.ring::after {
  content: "";
  position: absolute;
  inset: -17px;
  border: 3px dashed #ff7597;
  border-radius: 50%;
  box-shadow: 0 0 20px #ff174f;
}

.ring::after {
  inset: 12px;
  border-color: #ff174f;
  border-style: dotted;
  animation: rotate 3s linear infinite reverse;
}

.core {
  position: absolute;
  inset: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 75px;
  filter: drop-shadow(0 0 20px #ff174f);
  animation: float 2s ease-in-out infinite alternate;
}

.particle {
  position: absolute;
  width: 5px;
  height: 5px;
  background: #ff416d;
  border-radius: 50%;
  box-shadow: 0 0 12px 3px #ff174f;
  animation: fly 3s linear infinite;
}

@keyframes rotate {
  to { transform: rotate(360deg); }
}

@keyframes breathe {
  from { scale: 0.94; }
  to { scale: 1.05; }
}

@keyframes float {
  from { transform: translateY(-8px); }
  to { transform: translateY(8px); }
}

@keyframes pulse {
  from { opacity: 0.5; }
  to {
    opacity: 1;
    text-shadow: 0 0 25px #ff174f;
  }
}

@keyframes fly {
  0% {
    transform: translateY(100px) scale(0);
    opacity: 0;
  }
  50% { opacity: 1; }
  100% {
    transform: translateY(-220px) scale(1.8);
    opacity: 0;
  }
}
</style>
</head>

<body>
<div class="scene">
  <h1 class="title">ANIME ENERGY</h1>

  <div class="ring">
    <div class="core">⚡</div>
  </div>
</div>

<script>
const scene = document.querySelector(".scene");

for (let i = 0; i < 45; i++) {
  const p = document.createElement("div");
  p.className = "particle";

  p.style.left = Math.random() * 100 + "%";
  p.style.top = Math.random() * 100 + "%";
  p.style.animationDelay = Math.random() * 3 + "s";
  p.style.animationDuration = 2 + Math.random() * 3 + "s";

  scene.appendChild(p);
}
</script>
</body>
</html>
