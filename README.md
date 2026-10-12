
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Neon Heart Animation</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    background: #000;
    overflow: hidden;
    font-family: Arial, sans-serif;
}

canvas {
    display: block;
    width: 100%;
    height: 100vh;
}

h1 {
    position: absolute;
    top: 12%;
    width: 100%;
    text-align: center;
    color: #00ff66;
    font-size: 27px;
    letter-spacing: 5px;
    text-shadow: 0 0 10px #00ff66,
                 0 0 25px #00ff66;
}
</style>
</head>

<body>

<h1>NEON HEART</h1>
<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

let w, h, particles = [];

function resize() {
    canvas.width = w = window.innerWidth;
    canvas.height = h = window.innerHeight;
    createParticles();
}

function heart(t) {
    return {
        x: 16 * Math.pow(Math.sin(t), 3),
        y: -(13 * Math.cos(t)
          - 5 * Math.cos(2*t)
          - 2 * Math.cos(3*t)
          - Math.cos(4*t))
    };
}

function createParticles() {
    particles = [];

    for (let i = 0; i < 1000; i++) {
        let t = Math.random() * Math.PI * 2;
        let p = heart(t);

        particles.push({
            x: w / 2 + p.x * 12,
            y: h / 2 + p.y * 12,
            size: Math.random() * 2 + 0.5,
            alpha: Math.random(),
            speed: Math.random() * 0.04 + 0.01
        });
    }
}

let progress = 0;

function animate() {
    ctx.fillStyle = "rgba(0, 0, 0, 0.18)";
    ctx.fillRect(0, 0, w, h);

    const scale = Math.min(w, h) / 35;
    const cx = w / 2;
    const cy = h / 2;

    // Glowing heart outline
    ctx.save();
    ctx.translate(cx, cy);
    ctx.scale(scale, scale);

    ctx.beginPath();

    for (let t = 0; t <= Math.PI * 2; t += 0.01) {
        const p = heart(t);

        if (t === 0) {
            ctx.moveTo(p.x, p.y);
        } else {
            ctx.lineTo(p.x, p.y);
        }
    }

    ctx.closePath();
    ctx.strokeStyle = "#00ff66";
    ctx.lineWidth = 0.25;
    ctx.shadowBlur = 18;
    ctx.shadowColor = "#00ff66";
    ctx.stroke();
    ctx.restore();

    // Glowing particles
    particles.forEach(p => {
        p.alpha += p.speed;

        if (p.alpha > 1) p.alpha = 0;

        ctx.beginPath();
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(0,255,100,${p.alpha})`;
        ctx.shadowBlur = 12;
        ctx.shadowColor = "#00ff66";
        ctx.fill();
    });

    progress += 0.025;
    requestAnimationFrame(animate);
}

window.addEventListener("resize", resize);
resize();
animate();
</script>

</body>
</html>
