<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Chúc mừng sinh nhật chị Linh 🎂</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(to right, #ffdde1, #ee9ca7);
      font-family: 'Segoe UI', sans-serif;
      color: #fff;
      overflow: hidden;
      text-align: center;
    }

    h1 {
      font-size: 3em;
      margin-top: 100px;
      animation: fadeInDown 2s ease;
    }

    p {
      font-size: 1.5em;
      animation: fadeInUp 3s ease;
    }

    .cake {
      margin: 40px auto;
      width: 150px;
      height: 200px;
      background: #ff69b4;
      border-radius: 10px;
      position: relative;
      animation: bounce 2s infinite;
    }

    .candle {
      width: 10px;
      height: 50px;
      background: yellow;
      position: absolute;
      top: -60px;
      left: 50%;
      transform: translateX(-50%);
      border-radius: 5px;
    }

    .flame {
      width: 20px;
      height: 20px;
      background: orange;
      border-radius: 50%;
      position: absolute;
      top: -20px;
      left: 50%;
      transform: translateX(-50%);
      animation: flicker 1s infinite alternate;
    }

    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }

    @keyframes flicker {
      0% { opacity: 1; transform: scale(1); }
      100% { opacity: 0.6; transform: scale(1.2); }
    }

    @keyframes fadeInDown {
      from { opacity: 0; transform: translateY(-50px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(50px); }
      to { opacity: 1; transform: translateY(0); }
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: -1;
    }
  </style>
</head>
<body>
  <h1>🎉 Chúc Mừng Sinh Nhật Chị Linh 🎂</h1>
  <p>Chúc chị tuổi mới luôn xinh đẹp, rực rỡ như pháo hoa!<br> Thành công – Hạnh phúc – Trọn vẹn mọi điều! 💖</p>

  <div class="cake">
    <div class="candle">
      <div class="flame"></div>
    </div>
  </div>

  <audio autoplay loop>
    <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mp3" />
    Trình duyệt của bạn không hỗ trợ nhạc nền.
  </audio>

  <canvas id="fireworks"></canvas>

  <script>
    // Pháo hoa
    const canvas = document.getElementById('fireworks');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const fireworks = [];

    function createFirework() {
      const x = Math.random() * canvas.width;
      const y = Math.random() * canvas.height / 2;
      const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff'];
      for (let i = 0; i < 100; i++) {
        fireworks.push({
          x,
          y,
          radius: Math.random() * 3 + 2,
          color: colors[Math.floor(Math.random() * colors.length)],
          angle: Math.random() * 2 * Math.PI,
          speed: Math.random() * 5 + 2,
          alpha: 1
        });
      }
    }

    function drawFireworks() {
      ctx.fillStyle = 'rgba(0,0,0,0.2)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);
      for (let i = 0; i < fireworks.length; i++) {
        const f = fireworks[i];
        const vx = Math.cos(f.angle) * f.speed;
        const vy = Math.sin(f.angle) * f.speed;
        f.x += vx;
        f.y += vy;
        f.alpha -= 0.01;

        ctx.beginPath();
        ctx.arc(f.x, f.y, f.radius, 0, 2 * Math.PI);
        ctx.fillStyle = `rgba(${hexToRgb(f.color)}, ${f.alpha})`;
        ctx.fill();
      }

      for (let i = fireworks.length - 1; i >= 0; i--) {
        if (fireworks[i].alpha <= 0) {
          fireworks.splice(i, 1);
        }
      }
    }

    function hexToRgb(hex) {
      hex = hex.replace('#', '');
      const bigint = parseInt(hex, 16);
      const r = (bigint >> 16) & 255;
      const g = (bigint >> 8) & 255;
      const b = bigint & 255;
      return `${r},${g},${b}`;
    }

    function loop() {
      drawFireworks();
      requestAnimationFrame(loop);
    }

    setInterval(createFirework, 1000);
    loop();
  </script>
</body>
</html>
