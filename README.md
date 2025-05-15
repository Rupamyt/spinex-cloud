# spinex-cloud

html_code = """<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Spinex Cloud - Minecraft Hosting</title>
  <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet" />
  <style>
    /* Basic Reset */
    * {
      margin: 0; padding: 0; box-sizing: border-box;
    }
    body, html {
      height: 100%;
      font-family: 'Press Start 2P', cursive;
      background: #0a0a0a;
      color: #00ff99;
      overflow: hidden;
      user-select: none;
    }
    /* Animated Minecraft pixel background */
    body::before {
      content: "";
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: url('https://media.tenor.com/qDgZuTWLnXMAAAAd/minecraft-scenery.gif') center center/cover no-repeat;
      filter: brightness(0.4);
      animation: bgPulse 8s infinite alternate ease-in-out;
      z-index: -2;
    }
    @keyframes bgPulse {
      0% { filter: brightness(0.4); }
      50% { filter: brightness(0.65); }
      100% { filter: brightness(0.4); }
    }
    /* Animated Logo */
    .logo {
      font-size: 3rem;
      text-align: center;
      margin: 50px 0 10px;
      letter-spacing: 0.2em;
      color: #00ff99;
      position: relative;
      animation: glow 2.5s ease-in-out infinite alternate;
    }
    .logo::after {
      content: '⛏️'; /* Pickaxe emoji for Minecraft vibe */
      position: absolute;
      right: -40px;
      top: 0;
      animation: swing 2s ease-in-out infinite alternate;
    }
    @keyframes glow {
      from {
        text-shadow:
          0 0 5px #00ff99,
          0 0 10px #00ff99,
          0 0 20px #00ff99,
          0 0 40px #00ff99;
        color: #00ff99;
      }
      to {
        text-shadow:
          0 0 10px #00ff99,
          0 0 20px #00ff99,
          0 0 40px #00ff99,
          0 0 80px #00ff99;
        color: #00ffcc;
      }
    }
    @keyframes swing {
      from { transform: rotate(0deg); }
      to { transform: rotate(20deg); }
    }
    /* Plans Section */
    .plans {
      display: flex;
      justify-content: center;
      gap: 40px;
      flex-wrap: wrap;
      padding: 30px;
    }
    .plan {
      background: rgba(0, 255, 153, 0.1);
      border: 2px solid #00ff99;
      border-radius: 12px;
      width: 280px;
      padding: 30px 20px;
      text-align: center;
      box-shadow: 0 0 15px #00ff99;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
      position: relative;
      overflow: hidden;
    }
    .plan:hover {
      transform: scale(1.05);
      box-shadow: 0 0 30px #00ff99, 0 0 60px #00ffcc;
    }
    /* Animated Button */
    .btn {
      margin-top: 25px;
      padding: 15px 30px;
      background: linear-gradient(45deg, #00ff99, #00cc77);
      border: none;
      border-radius: 8px;
      font-weight: 700;
      font-size: 1rem;
      color: #001100;
      cursor: pointer;
      box-shadow:
        0 0 10px #00ff99,
        0 0 20px #00cc77;
      transition: background 0.5s ease, box-shadow 0.5s ease;
      position: relative;
      overflow: hidden;
      z-index: 0;
    }
    .btn::before {
      content: "";
      position: absolute;
      top: 50%; left: 50%;
      width: 200%; height: 200%;
      background: rgba(255, 255, 255, 0.15);
      transform: translate(-50%, -50%) scale(0);
      border-radius: 50%;
      transition: transform 0.4s ease;
      z-index: -1;
    }
    .btn:hover::before {
      transform: translate(-50%, -50%) scale(1);
    }
    /* Click effect */
    .click-effect {
      position: absolute;
      border-radius: 50%;
      background: #00ff99;
      pointer-events: none;
      animation: clickAnim 0.5s forwards;
      opacity: 0.75;
      z-index: 1000;
    }
    @keyframes clickAnim {
      0% {
        transform: scale(1);
        opacity: 0.75;
      }
      100% {
        transform: scale(5);
        opacity: 0;
      }
    }
    /* Footer */
    footer {
      text-align: center;
      font-size: 12px;
      margin-top: 60px;
      color: #004422;
      text-shadow: 0 0 3px #00ff99;
      user-select: none;
    }
    /* Responsive */
    @media (max-width: 700px) {
      .plans {
        flex-direction: column;
        gap: 20px;
        padding: 10px;
      }
      .plan {
        width: 90%;
        margin: 0 auto;
      }
      .logo {
        font-size: 2.2rem;
        margin: 30px 0 10px;
      }
    }
  </style>
</head>
<body>
  <h1 class="logo">SPINEX CLOUD</h1>
  <section class="plans">
    <div class="plan" tabindex="0" role="button" aria-label="Starter Plan">
      <h2>Starter</h2>
      <p>2GB RAM<br>10 Slots<br>$3.99/month</p>
      <button class="btn" onclick="payNow('starter')">Buy Now</button>
    </div>
    <div class="plan" tabindex="0" role="button" aria-label="Pro Plan">
      <h2>Pro</h2>
      <p>4GB RAM<br>20 Slots<br>$7.99/month</p>
      <button class="btn" onclick="payNow('pro')">Buy Now</button>
    </div>
    <div class="plan" tabindex="0" role="button" aria-label="Ultimate Plan">
      <h2>Ultimate</h2>
      <p>8GB RAM<br>50 Slots<br>$14.99/month</p>
      <button class="btn" onclick="payNow('ultimate')">Buy Now</button>
    </div>
  </section>

  <footer>© 2025 Spinex Cloud — Minecraft Hosting</footer>

  <script>
    // Click animation on body clicks
    document.body.addEventListener('click', function(e) {
      const circle = document.createElement('span');
      circle.classList.add('click-effect');
      circle.style.left = e.pageX + 'px';
      circle.style.top = e.pageY + 'px';
      document.body.appendChild(circle);
      setTimeout(() => circle.remove(), 500);
    });

    // Mock payment function
    function payNow(plan) {
      alert(`Redirecting to payment for the ${plan.toUpperCase()} plan.`);
      // Add real payment integration here
    }
  </script>
</body>
</html>"""

zip_path = "/mnt/data/spinex_cloud_minecraft_hosting.zip"

with zipfile.ZipFile(zip_path, 'w') as zip_file:
    zip_file.writestr("index.html", html_code)

zip_path
