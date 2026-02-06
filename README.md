<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  < title>Who will win the biggest battle ever!</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, sans-serif;
    }

    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background: radial-gradient(circle at top, #0f172a, #020617);
      color: #e5e7eb;
      overflow: hidden;
    }

    .container {
      text-align: center;
    }

    h1 {
      font-size: clamp(1.5rem, 4vw, 3rem);
      margin-bottom: 2rem;
      text-shadow: 0 2px 10px rgba(0,0,0,0.5);
    }

    .arena {
      position: relative;
      width: min(90vw, 600px);
      height: 300px;
      margin: 0 auto;
      border-radius: 20px;
      background: rgba(255,255,255,0.05);
      box-shadow: inset 0 0 0 1px rgba(255,255,255,0.1);
      overflow: hidden;
    }

    button {
      position: absolute;
      padding: 14px 24px;
      font-size: 1.2rem;
      border-radius: 999px;
      border: none;
      cursor: pointer;
      transition: transform 0.15s ease, box-shadow 0.15s ease;
      box-shadow: 0 6px 20px rgba(0,0,0,0.3);
      user-select: none;
    }

    #dadBtn {
      left: 50%;
      top: 65%;
      transform: translate(-50%, -50%);
      background: linear-gradient(135deg, #22c55e, #16a34a);
      color: #052e16;
      font-weight: 700;
    }

    #dadBtn:hover {
      transform: translate(-50%, -50%) scale(1.05);
      box-shadow: 0 10px 30px rgba(34,197,94,0.5);
    }

    #ilyasBtn {
      left: 50%;
      top: 30%;
      transform: translate(-50%, -50%);
      background: linear-gradient(135deg, #38bdf8, #0ea5e9);
      color: #082f49;
      font-weight: 700;
      pointer-events: none; /* just in case — this one is never meant to be clicked */
    }

    /* Celebration overlay */
    .celebration {
      position: fixed;
      inset: 0;
      pointer-events: none;
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 10;
    }

    .celebration.active {
      display: flex;
    }

    .winner {
      font-size: clamp(2rem, 6vw, 4rem);
      font-weight: 900;
      color: #22c55e;
      text-shadow: 0 4px 20px rgba(34,197,94,0.7);
      animation: pop 0.6s ease-out;
    }

    @keyframes pop {
      0% { transform: scale(0.5); opacity: 0; }
      70% { transform: scale(1.1); opacity: 1; }
      100% { transform: scale(1); }
    }

    canvas {
      position: fixed;
      inset: 0;
      pointer-events: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Who will win the biggest battle ever!</h1>
    <div class="arena" id="arena">
      <button id="ilyasBtn">ilyas 🥷</button>
      <button id="dadBtn">Dad 💪</button>
    </div>
  </div>

  <div class="celebration" id="celebration">
    <div class="winner">Dad Wins! 💪🎉</div>
  </div>

  <canvas id="confetti"></canvas>

  <script>
    const arena = document.getElementById("arena");
    const ilyasBtn = document.getElementById("ilyasBtn");
    const dadBtn = document.getElementById("dadBtn");
    const celebration = document.getElementById("celebration");

    // Make the "ilyas" button run away when the mouse gets near
    arena.addEventListener("mousemove", (e) => {
      const rect = arena.getBoundingClientRect();
      const btnRect = ilyasBtn.getBoundingClientRect();

      const mouseX = e.clientX;
      const mouseY = e.clientY;

      const btnX = btnRect.left + btnRect.width / 2;
      const btnY = btnRect.top + btnRect.height / 2;

      const dx = mouseX - btnX;
      const dy = mouseY - btnY;
      const distance = Math.hypot(dx, dy);

      const dangerRadius = 120; // how close is "too close"

      if (distance < dangerRadius) {
        // Move button to a random safe spot inside the arena
        const arenaWidth = rect.width;
        const arenaHeight = rect.height;

        const padding = 20;
        const newX = Math.random() * (arenaWidth - btnRect.width - padding * 2) + padding;
        const newY = Math.random() * (arenaHeight - btnRect.height - padding * 2) + padding;

        ilyasBtn.style.left = newX + "px";
        ilyasBtn.style.top = newY + "px";
        ilyasBtn.style.transform = "translate(0, 0)";
      }
    });

    // Celebration when Dad is clicked
    dadBtn.addEventListener("click", () => {
      celebration.classList.add("active");
      startConfetti();
    });

    // Simple confetti animation
    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener("resize", resizeCanvas);
    resizeCanvas();

    let confettiPieces = [];

    function startConfetti() {
      confettiPieces = [];
      const colors = ["#22c55e", "#38bdf8", "#facc15", "#fb7185", "#a78bfa"];

      for (let i = 0; i < 200; i++) {
        confettiPieces.push({
          x: Math.random() * canvas.width,
          y: -20,
          size: Math.random() * 8 + 4,
          speedY: Math.random() * 3 + 2,
          speedX: (Math.random() - 0.5) * 2,
          color: colors[Math.floor(Math.random() * colors.length)],
          rotation: Math.random() * Math.PI
        });
      }

      requestAnimationFrame(updateConfetti);
    }

    function updateConfetti() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      confettiPieces.forEach(p => {
        p.y += p.speedY;
        p.x += p.speedX;
        p.rotation += 0.1;

        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.rotate(p.rotation);
        ctx.fillStyle = p.color;
        ctx.fillRect(-p.size / 2, -p.size / 2, p.size, p.size);
        ctx.restore();
      });

      confettiPieces = confettiPieces.filter(p => p.y < canvas.height + 20);

      if (confettiPieces.length > 0) {
        requestAnimationFrame(updateConfetti);
      }
    }
  </script>
</body>
</html>
